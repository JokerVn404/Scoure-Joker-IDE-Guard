# User Guide — Scoure v0.1.0

This guide shows how to use Scoure as an end user (non-developer).

---

## Installation

### Windows

1. Download installer from Releases.
2. Run PowerShell (as Administrator):
   ```powershell
   .\install-native-host.ps1 -ExtensionId "your-ext-id" -Scope User
   ```
3. Add Chrome extension (via Chrome Web Store or load unpacked).
4. Restart Chrome.

### macOS / Linux

```bash
./installers/install-native-host.sh --ext-id "your-ext-id" --scope user
```

---

## First-time Setup

1. Open extension popup (Chrome icon).
2. Click "Setup" or "First Time".
3. Read consent popup (explains what is collected + stored locally).
4. Click "I Agree" to enable plugin registration.
5. Plugin will save consent locally + register with API.

---

## Capture workflows

### Workflow 1: Capture web content (Chrome extension)

1. Select text on a webpage (or copy URL).
2. Click extension icon → "Capture Selection" or "Capture Page".
3. Extension shows preview in popup panel.
4. Click "Upload" when ready.
5. Capture is sent to API + stored in your evidence library.

### Workflow 2: Capture project files (Plugin local)

1. Open terminal in your project folder.
2. Run: `npm run plugin -- capture`
3. Select files/folders to snapshot.
4. Review in terminal UI.
5. Click "Upload" to send to API.

### Workflow 3: Manual upload

1. Create a file or screenshot.
2. Open extension → "Upload file".
3. Select file + add metadata (optional).
4. Review + approve consent popup.
5. Click "Upload".

---

## Review & manage captures

### In extension:

1. Click extension icon → "Review Captures".
2. Lists all local captures (metadata only).
3. Options:
   - View hash / metadata.
   - Delete locally (no recovery).
   - Mark for upload.

### In API Dashboard (if available):

1. Login to dashboard.
2. "My Evidence" tab.
3. View uploaded evidence metadata.
4. Cannot view raw content (only metadata) unless explicitly requested.

---

## Privacy & consent

**What Scoure collects (locally, on your device):**
- File snapshots (you select which files).
- Text you copy/paste or select on web.
- Screenshots (you trigger).
- Metadata: path, URL, timestamp, hash.

**What Scoure sends to cloud (if you approve upload):**
- Metadata (hash, timestamp, path).
- Consent proof (proof you agreed).
- Content (encrypted, stored safely).

**What Scoure DOES NOT collect:**
- Background auto-capture (unless you enable it explicitly).
- Personal information (emails, passwords, PII) — you must manually exclude.
- System data beyond what you capture.

**Deleting data:**
- Delete local captures anytime (extension UI or file browser).
- Revoke plugin registration anytime (removes cloud metadata + consent).
- Request data deletion from API (support@example.com).

---

## Troubleshooting

### Extension won't load in Chrome

- Check that `manifest.json` exists in extension folder.
- Verify extension ID matches in native host registration.
- Reload extension (chrome://extensions → Reload button).

### Native host not communicating

- Verify native host process is running (see SETUP.md).
- Check Windows Firewall / macOS security settings.
- Restart Chrome and native host.

### Captures not encrypting / uploading

- Check local storage permissions (AppData folder on Windows).
- Verify API server is running and reachable.
- Check browser console for errors (F12).

### Consent popup not appearing

- First-time only. If dismissed, manually clear local storage:
  - Windows: `%LOCALAPPDATA%\Scoure\consent.json`.
  - macOS/Linux: `~/.scoure/consent.json`.
- Restart extension.

### Windows Defender / Antivirus blocking

- See SETUP.md > Antivirus section for verification + allowlisting steps.
