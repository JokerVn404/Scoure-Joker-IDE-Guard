# Privacy Policy & Data Handling — Scoure v0.1.0

**Last updated:** 2024-01-01  
**Version:** v0.1.0 MVP

---

## Overview

Scoure is designed with **privacy-first** principles. We minimize data collection, store sensitive information locally on your device, and **never** collect data without explicit user consent.

**Core principle:** User controls what is captured, what is stored, and when it is uploaded.

---

## What We Collect

### Locally on Your Device (Encrypted, No Cloud)

When you use Scoure plugin or extension, the following is stored **only on your device**, encrypted at rest:

- **Captured content:** Text you select, files you snapshot, screenshots you take.
- **Metadata:** Paths, URLs, timestamps, hashes (SHA-256).
- **Session info:** Project IDs, session IDs, capture dates.
- **Consent records:** Local reference to consent agreement (timestamps, scope).

**Storage locations:**
- Windows: `%LOCALAPPDATA%\Scoure\` (encrypted with Windows DPAPI).
- macOS: `~/.scoure/` (encrypted with Keychain).
- Linux: `~/.scoure/` (encrypted with secret-service).

**Encryption:** AES-256-GCM (authenticated encryption).

### In Cloud (Only if User Uploads & Consents)

When you explicitly click **"Upload"** and approve consent, the following is sent to Scoure API:

- **Content hash:** SHA-256 hash of captured content (no content itself).
- **Metadata:** Path, URL, title, timestamp, evidence type.
- **Consent proof:** Consent ID + signature (proves you agreed).
- **Minimal project info:** Project ID, session ID (no personal data).

**Not sent to cloud:**
- ❌ Raw captured content (unless explicitly uploaded by you).
- ❌ Personal information (emails, passwords, PII) — you must manually exclude.
- ❌ System data beyond what you captured.
- ❌ Background auto-capture logs (we don't auto-capture).

---

## Consent Model (Critical)

### What is Consent?

Before using Scoure, you must **explicitly agree** to what we collect and how we use it.

### Consent Scopes (User Chooses)

1. **"Store locally encrypted"** — captures stored on your device, encrypted.
   - Default: ✅ ON (always asked first).
   - Revoke: Delete local folder `~/.scoure/`.

2. **"Heartbeat"** — periodically send "I'm still here" signal (plugin/extension alive).
   - Default: ⭕ OFF (user opt-in).
   - If enabled: sends only `plugin_id + timestamp` to API.

3. **"Auto-upload on approval"** — automatically upload after user approves in UI.
   - Default: ⭕ OFF (user opt-in).
   - If enabled: uploads after user clicks "Upload" button.

### First-Run Consent Popup

On first use, you will see a popup explaining what we collect and how we store it.

### Revoking Consent

You can revoke consent anytime:

```bash
# Revoke plugin registration
npm run cli -- revoke-consent

# OR manually delete consent file
rm ~/.scoure/consent.json
```

When revoked:
- Extension/plugin stops uploading.
- Cloud registration is marked inactive.
- Local captures remain on your device (encrypted).

---

## Data Retention

### Local Retention (Your Control)

- **Indefinite** — captures stored locally until YOU delete them.
- Delete method:
  - Extension UI: "Delete locally" button.
  - CLI: `npm run cli -- delete-capture <id>`.
  - Manual: delete file from `~/.scoure/captures/`.

### Cloud Retention (If Uploaded)

- **Indefinite** — uploaded evidence stored in your account.
- Delete method:
  - API: DELETE /v1/evidence/{id} (requires authentication).
  - Request deletion: email support@scoure.example.com.
  - Compliance: GDPR "right to be forgotten" honored within 30 days.

**Note:** We keep cryptographic proof of deletion (hash record) for audit purposes but destroy all content.

---

## Data Security

### Encryption

- **Local:** AES-256-GCM with keys derived from OS Keychain.
- **Transit:** TLS 1.3 (HTTPS).
- **Cloud:** Encrypted at rest (AWS S3 SSE-S3 or KMS).

### Authentication

- **User login:** OAuth2 or JWT tokens (no passwords stored).
- **Plugin/extension:** API keys with scoped permissions + short TTL.
- **Evidence upload:** Signed with plugin key (proves authenticity).

### Audit Logging

- **API logs:** All uploads, access, deletions logged.
- **Immutable log:** Append-only audit trail; cannot be edited.
- **Access control:** Admins only; users cannot view API logs (privacy protection).

---

## Third Parties & Data Sharing

### Do We Share Data?

**Short answer: No** (except as required by law).

- ❌ We do **not** sell your data.
- ❌ We do **not** share data with advertisers.
- ❌ We do **not** use data for ML training (v1; v2+ may offer opt-in analytics).
- ✅ We **may** share data if legally required (e.g., law enforcement with warrant).

### External Services (v1)

- **Cloud provider:** AWS (S3 + RDS for storage). See AWS privacy policy.
- **Optional future (v2+):** ML embedding service (if user opts-in).

---

## Special Considerations

### PII (Personally Identifiable Information)

**Scoure does NOT automatically redact PII.** If your captures contain:
- Emails, phone numbers, names, addresses.
- API keys, passwords, secret tokens.

**You are responsible** for excluding or redacting before uploading.

**Recommendation:** Review capture UI before upload; Scoure will warn if content looks like PII (future feature, v2+).

### Code / Intellectual Property

Scoure stores snapshots of code/documentation you capture. This is **your data**; we do not claim rights to it.

---

## Compliance & Legal

### GDPR (EU Users)

- ✅ **Data minimization:** We collect only what you capture.
- ✅ **User control:** You can delete anytime.
- ✅ **Transparency:** This policy explains what we do.
- ✅ **Right to erasure:** Honored within 30 days.
- ✅ **Data processing:** We act as data processor; you (or your org) are data controller.

### CCPA (California Users)

- ✅ **Right to know:** You can request data download (future feature).
- ✅ **Right to delete:** You can request deletion.
- ✅ **No selling:** We do not sell personal information.

### Other Jurisdictions

This policy applies globally. If your jurisdiction has stricter requirements, those apply.

---

## Policy Changes

We may update this policy. Changes will be announced via:
- Email (if you have an account).
- GitHub releases (README update).
- In-app notification (future).

Continued use of Scoure after changes means you accept new policy.

---

## Questions or Concerns?

- **Privacy inquiry:** privacy@scoure.example.com
- **Data deletion request:** support@scoure.example.com
- **GitHub issues:** [Issues](https://github.com/JokerVn404/Scoure-Joker-IDE-Guard/issues)
