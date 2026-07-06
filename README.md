# Scoure - AI IDEA GUARD

**Digital Provenance & Evidence Platform** — Version: **0.1.0 (MVP)**

Scoure là nền tảng giúp quản lý nguồn gốc (provenance) và bằng chứng kỹ thuật của ý tưởng, tài liệu và mã nguồn khi làm việc với các công cụ AI. Hệ thống thu thập bằng chứng từ plugin local và Chrome extension, lưu trữ local-first (encrypted), và cho phép upload để phân tích khi người dùng đồng ý.

**v0.1.0 MVP focus:** Plugin local + Chrome extension + minimal API để test end-to-end capture → store → upload flow. Scoring logic và community board sẽ là v2.

---

## 🎯 Mục tiêu v1

- ✅ Plugin local: snapshot project files, compute hash, store encrypted locally.
- ✅ Chrome extension: capture web/chat, store local, review + upload.
- ✅ Consent & privacy: explicit opt-in, no background cloud logging, user controls data.
- ✅ Native host: communicate between extension/plugin and optional sidecar agent.
- ✅ Minimal API: ingest evidence, register plugin, store metadata.
- ⏳ v2: scoring, comparator, public board, VS Code / Coder plugin.

---

## 🏗️ Kiến trúc v1 (tóm tắt)

```
Plugin Local (Node.js CLI)
    ↓ (native messaging / stdio)
Native Host (Node.js service)
    ↓ (HTTP POST)
Shared Core API (Express + Postgres + S3)
    ↓
Dashboard (minimal, JSON read)

Chrome Extension (webview)
    ↓ (native messaging / POST)
Shared Core API
    ↓
Local Storage (encrypted, device-only)
```

**Data flow:**
1. User triggers capture (in plugin or extension).
2. Capture stored locally encrypted (%LOCALAPPDATA%\Scoure or ~/.scoure).
3. User reviews capture in UI.
4. On upload approval: evidence POSTed to /v1/evidence with consent proof.
5. API stores metadata + signs + returns receipt.
6. Dashboard displays minimal info (metadata only, not content).

---

## 📋 Quick Start

### Prerequisites
- Node.js 16+ (for native host & backend).
- npm / yarn.
- Chrome/Edge browser (for extension).
- (Optional) Postgres + MinIO/S3 for dev server.

### Installation (Developer)

```bash
# Clone repo
git clone https://github.com/JokerVn404/Scoure-Joker-IDE-Guard.git
cd Scoure-Joker-IDE-Guard
git checkout feat/v1-complete

# Install dependencies (backend)
cd server
npm install

# Install dependencies (native host)
cd ../native-host
npm install

# Install dependencies (extension)
cd ../extension
npm install
```

### Run v1 end-to-end (dev mode)

```bash
# Terminal 1: Backend API
cd server
npm run dev
# API listens on http://localhost:8080

# Terminal 2: Native host (standalone)
cd native-host
npm start
# Host listens on stdio or localhost:9000 (see config)

# Terminal 3: Load extension in Chrome
# Open chrome://extensions -> Load unpacked -> select ./extension folder
```

### First test: Capture & Upload

```bash
# 1. Via native host CLI
cd native-host
npm run cli -- capture --path "/path/to/project" --consent-id "<uuid>"

# 2. Via Chrome extension
# - Open extension popup
# - Select text or URL
# - Click "Capture"
# - Review in panel
# - Click "Upload"

# 3. Check API
curl http://localhost:8080/v1/evidence | jq
```

---

## 🔒 Privacy & Consent (v1 critical)

**User-consent first:**
- ✅ No auto-capture; only on explicit user action.
- ✅ No 24/7 background cloud logging; local storage by default.
- ✅ Consent record saved server-side (proof of user agreement).
- ✅ User can delete local captures anytime.

**What is stored locally (encrypted AES-256):**
- Captured content (text, screenshots, file snippets).
- Metadata (path, URL, timestamp, hash).
- Consent references.

**What is stored in cloud (minimal metadata only, if user consented):**
- Project ID, session ID, first prompt hash.
- Plugin ID, last-seen timestamp.
- Content hash (no content itself).
- Consent record (who, when, scope).

**User controls:**
- Can review all local captures before upload.
- Can delete local captures anytime (no cloud recovery).
- Can revoke plugin/extension registration anytime.

See **PRIVACY.md** for details.

---

## 📚 Documentation

- **[ARCHITECTURE.md](ARCHITECTURE.md)** — system design, components, data model.
- **[API.md](API.md)** — API endpoints, request/response examples.
- **[SETUP.md](SETUP.md)** — dev environment, build, test.
- **[USAGE.md](USAGE.md)** — user guide, step-by-step workflows.
- **[PRIVACY.md](PRIVACY.md)** — privacy policy, consent model, retention.
- **[CONTRIBUTING.md](CONTRIBUTING.md)** — how to contribute.
- **[BUILD.md](BUILD.md)** — build & test instructions.

---

## 🔧 Tech Stack (v1)

- **Backend:** Node.js, Express, Postgres, S3-compatible storage.
- **Native Host:** Node.js (stdio + JSON message protocol).
- **Chrome Extension:** TypeScript, Webpack, Chrome Extension Manifest v3.
- **Local Storage:** AES-256 encryption, OS Keychain (Windows DPAPI, macOS Keychain, Linux secret-service).
- **Installer:** PowerShell scripts (Windows), shell scripts (macOS/Linux).

---

## 🚀 Deployment (v1 early)

### For developers:
- Clone, npm install, npm run dev (see SETUP.md).
- Test locally with Chrome extension loaded unpacked.

### For users (beta):
- (Coming soon) Pre-built extension on Chrome Web Store (pending review).
- (Coming soon) Native host downloadable from Releases.
- Windows installer: PowerShell script (see installers/).

---

## 📊 Roadmap

### v0.1.0 (Current - MVP)
- ✅ Plugin local (Node.js CLI).
- ✅ Chrome extension (capture + local store + upload).
- ✅ Minimal API (ingest, register, store).
- ✅ Consent & privacy enforcement.

### v0.2.0 (Next)
- Comparator logic (hash match, token diff).
- Scoring policy.
- Basic report generation (JSON).
- Dashboard UI (minimal).

### v1.0.0 (Later)
- ML-based similarity (embeddings).
- Public board (redacted reports).
- Community evaluation features.
- VS Code extension.
- Coder (code-server) plugin.

---

## ❓ FAQ

**Q: Is my data safe?**  
A: Local captures are encrypted on your device. We only store minimal metadata in cloud if you consent. See PRIVACY.md.

**Q: Will the plugin modify my code?**  
A: No. Plugin is read-only. It only snapshots and hashes; never edits or injects.

**Q: Can I delete my data?**  
A: Yes. Delete local captures anytime. Revoke plugin/extension anytime. See USAGE.md.

**Q: What if Windows Defender flags the plugin?**  
A: Plugin is unsigned (v1). See SETUP.md > "Antivirus" section for verification steps.

---

## 📞 Support & Community

- **Issues:** [GitHub Issues](https://github.com/JokerVn404/Scoure-Joker-IDE-Guard/issues)
- **Discussions:** [GitHub Discussions](https://github.com/JokerVn404/Scoure-Joker-IDE-Guard/discussions)
- **Security:** See SECURITY.md (coming soon).

---

## 📄 License

Proprietary. See LICENSE and COPYING.md.

---

## Authors & Contributors

- **JokerVn404** — Project lead, architecture.
- Contributors welcome (private phase).
