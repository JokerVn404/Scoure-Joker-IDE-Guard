# Architecture — Scoure v0.1.0 MVP

## System Overview

Scoure v1 is a **local-first, evidence-capture system** with three main components:

```
┌─────────────────────────────────────────────────────────────────┐
│                      User Environment                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                   │
│  ┌──────────────────┐          ┌──────────────────┐             │
│  │  Plugin Local    │          │ Chrome Extension │             │
│  │  (Node.js CLI)   │          │  (TypeScript)    │             │
│  │                  │          │                  │             │
│  │ • Snapshot files │          │ • Capture web    │             │
│  │ • Compute hash   │          │ • Screenshot     │             │
│  │ • Local store    │          │ • Text select    │             │
│  │ • Consent UI     │          │ • URL            │             │
│  └────────┬─────────┘          └────────┬─────────┘             │
│           │                              │                      │
│           └──────────────┬───────────────┘                       │
│                          │                                       │
│                    ┌─────▼──────────┐                            │
│                    │  Native Host   │                            │
│                    │  (Node.js)     │                            │
│                    │                │                            │
│                    │ • Encrypt/sign │                            │
│                    │ • Local queue  │                            │
│                    │ • Upload mgmt  │                            │
│                    └─────┬──────────┘                            │
└─────────────────────────┼────────────────────────────────────────┘
                          │ (HTTPS + TLS)
                          │
        ┌─────────────────▼──────────────────┐
        │      Shared Core API (v1 minimal)   │
        ├────────────────────────────────────┤
        │  • POST /v1/evidence (ingest)       │
        │  • POST /v1/plugins/register        │
        │  • POST /v1/plugins/heartbeat       │
        │  • GET /v1/evidence/{id}            │
        │  • Authentication & audit log       │
        └──────────────┬──────────────────────┘
                       │
        ┌──────────────┴──────────────┐
        │                             │
    ┌───▼────┐                  ┌────▼────┐
    │Postgres │                │   S3 /   │
    │ (meta)  │                │  MinIO   │
    │         │                │ (objects)│
    └─────────┘                └──────────┘
```

---

## Component Details

### 1. Plugin Local (Node.js CLI)

**Purpose:** Snapshot project files, compute hashes, store locally, manage consent.

**Key features:**
- CLI commands: `scoure capture`, `scoure review`, `scoure upload`.
- Scan workspace (user selects files/dirs).
- Compute SHA256 hash + metadata.
- Store encrypted locally (%LOCALAPPDATA%\Scoure or ~/.scoure).
- First-run consent popup (show scope + data handling).
- Consent record saved locally + reference sent to API.

**Data stored locally (encrypted AES-256):**
```
~/.scoure/
  ├── captures/
  │   ├── <uuid-1>.enc
  │   ├── <uuid-2>.enc
  │   └── ...
  ├── metadata.json (index, encrypted)
  ├── consent.json (references)
  └── config.json (settings, encrypted keys)
```

**Consent model:**
- On first use: show popup with scope (e.g., "Store snapshots locally, allow heartbeat?").
- Save consent_id locally + POST to /v1/projects/{id}/plugins/register.
- All uploads include consent_id as proof.

---

### 2. Chrome Extension (TypeScript + Manifest v3)

**Purpose:** Capture web content (text, screenshots, URLs) with user consent.

**Key features:**
- Popup UI: show options (capture selection, capture page, capture current tab).
- Capture types: text selection, full page screenshot, URL + title, chat history (if permitted).
- Store captures encrypted locally (Chrome storage.local).
- Review panel: show captured items, metadata, allow delete.
- Upload trigger: POST to /v1/evidence with consent proof.
- No auto-capture (user action only).

**Manifest structure:**
```json
{
  "manifest_version": 3,
  "name": "Scoure Capture",
  "permissions": ["storage", "activeTab", "scripting", "webRequest"],
  "host_permissions": ["https://*/*", "http://*/*"],
  "background": { "service_worker": "background.js" },
  "action": { "default_popup": "popup.html" }
}
```

**Storage (Chrome storage.local, encrypted):**
```
{
  "captures": [
    {
      "id": "<uuid>",
      "type": "screenshot|text|url",
      "content_hash": "sha256:...",
      "timestamp": "2024-...",
      "metadata": { "url": "...", "title": "...", "selected_text": "..." },
      "status": "pending|uploaded"
    }
  ],
  "consent": { "id": "<consent-uuid>", "scope": [...] }
}
```

---

### 3. Native Host (Node.js)

**Purpose:** IPC bridge + agent for plugin ↔ extension ↔ API communication.

**Key features:**
- Listen on stdio (standard native messaging) or localhost port (HTTP).
- Receive capture requests from extension/plugin.
- Encrypt/sign evidence locally.
- Queue uploads; retry on network failure.
- Communicate with Shared Core API.
- Log audit trail (timestamps, operations, consents).

**Communication protocol (stdio, JSON lines):**
```json
// Request
{ "method": "capture", "payload": { "content": "...", "metadata": {...} }, "consent_id": "..." }

// Response
{ "id": "<uuid>", "status": "stored", "signed": true }
```

---

### 4. Shared Core API (Express + Postgres + S3)

**Purpose:** Minimal ingest, authentication, evidence storage, audit logging.

**Key endpoints (v1):**
- `POST /v1/evidence` — store evidence (multipart: metadata JSON + file).
- `POST /v1/projects/{id}/plugins/register` — register plugin + consent.
- `POST /v1/plugins/{id}/heartbeat` — optional heartbeat (if user consented).
- `GET /v1/evidence/{id}` — retrieve metadata (not content).
- `POST /auth/login` — user auth (OAuth/JWT).

**Data model (Postgres):**
```sql
-- Projects
CREATE TABLE projects (
  id UUID PRIMARY KEY,
  owner_id VARCHAR NOT NULL,
  name VARCHAR NOT NULL,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Evidence units
CREATE TABLE evidence (
  id UUID PRIMARY KEY,
  project_id UUID NOT NULL REFERENCES projects(id),
  type VARCHAR NOT NULL, -- 'file', 'text', 'screenshot'
  content_hash VARCHAR NOT NULL, -- sha256 hex
  uri VARCHAR, -- s3://...
  metadata JSONB, -- { path, url, title, timestamp, ... }
  redaction_status VARCHAR DEFAULT 'none', -- none, partial, public
  signatures JSONB, -- [{ method, value, signed_by, key_id }]
  created_at TIMESTAMP DEFAULT NOW(),
  FOREIGN KEY (project_id) REFERENCES projects(id)
);

-- Consent records
CREATE TABLE consents (
  id UUID PRIMARY KEY,
  user_id VARCHAR NOT NULL,
  project_id UUID NOT NULL REFERENCES projects(id),
  scope VARCHAR[] NOT NULL, -- ['register', 'heartbeat', 'upload']
  text_version VARCHAR NOT NULL,
  accepted_at TIMESTAMP DEFAULT NOW(),
  expires_at TIMESTAMP
);

-- Audit log
CREATE TABLE audit_log (
  id BIGSERIAL PRIMARY KEY,
  user_id VARCHAR,
  action VARCHAR NOT NULL,
  resource_type VARCHAR,
  resource_id VARCHAR,
  details JSONB,
  timestamp TIMESTAMP DEFAULT NOW()
);
```

**S3 storage:**
- Store raw content (encrypted at rest).
- Path: `s3://scoure-bucket/projects/{projectId}/evidence/{evidenceId}/content`.

---

## Data Flow (v1 end-to-end)

### Scenario: User captures file in plugin local, uploads to API

```
1. User runs: npm run cli -- capture --path /my/project
   └─> Plugin scans files, shows consent UI

2. User clicks "I agree"
   └─> Consent_id generated, saved locally + POSTed to /v1/projects/{id}/plugins/register
       Server saves consent record, returns ack

3. Plugin snapshots selected files
   └─> Compute SHA256 hash, store encrypted locally

4. User reviews captures in CLI UI or webview panel
   └─> Lists captured items, metadata only

5. User clicks "Upload"
   └─> Native host encrypts evidence, POSTs to /v1/evidence
       Payload: { metadata: { consent_id, type, hash, ... }, file: <binary> }

6. API receives POST /v1/evidence
   └─> Validates consent_id
   └─> Stores file to S3
   └─> Saves metadata to Postgres
   └─> Signs evidence with KMS key
   └─> Returns { id, stored: true }

7. Extension/plugin receives ack
   └─> Marks local capture as "uploaded"
   └─> Clears local file (optionally) or keeps backup

8. User can review via Dashboard (API /v1/evidence/{id})
   └─> Returns metadata only (no content unless requested + approved)
```

---

## Security & Privacy (v1)

- **Encryption at rest:** AES-256 for local captures; local keys stored in OS Keychain.
- **Encryption in transit:** TLS 1.3 for all HTTP/HTTPS.
- **Authentication:** JWT tokens for API (user); API keys for agents (plugin/extension).
- **Consent proof:** Consent_id + signature on every upload; server verifies.
- **Audit logging:** Append-only; all actions logged (who, what, when).
- **No background logging:** No 24/7 cloud sync; only on explicit upload.

---

## Deployment (v1)

### Dev environment:
- Local Express server on http://localhost:8080.
- SQLite or local Postgres for dev DB.
- Local filesystem for "S3" storage (or MinIO).

### Staging/Beta:
- Containerized backend (Docker).
- Real Postgres + S3 (AWS or MinIO).
- TLS certificates (self-signed or Let's Encrypt).

### Production (later):
- K8s or serverless (Lambda, Cloud Run).
- RDS + S3.
- Domain + wildcard certs.
- Monitoring, backup, disaster recovery.

---

## What's NOT in v1

- ❌ Scoring / comparator logic.
- ❌ ML embeddings / similarity.
- ❌ Public report publishing.
- ❌ Community features.
- ❌ Code signing (certificates).
- ❌ VS Code / Coder plugin.
- ❌ Mobile support.

These are planned for v0.2+ / v1.0.
