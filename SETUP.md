# Development Setup — Scoure v0.1.0

This guide covers setting up the development environment to build, test, and run Scoure locally.

---

## Prerequisites

### Required

- **Node.js 16+** (LTS recommended)
- **npm** or **yarn**
- **Git**
- **Postgres 12+** (for backend; SQLite works for local dev)
- **(Optional) MinIO** or AWS S3 credentials (for object storage)

### Platform-specific

- **Windows:** PowerShell 5.0+, Windows 7+
- **macOS:** macOS 10.14+, Xcode Command Line Tools
- **Linux:** Ubuntu 18.04+, curl, git

---

## Installation

### Step 1: Clone Repository

```bash
git clone https://github.com/JokerVn404/Scoure-Joker-IDE-Guard.git
cd Scoure-Joker-IDE-Guard
git checkout feat/v1-complete
```

### Step 2: Install Backend Dependencies

```bash
cd server
npm install
```

### Step 3: Install Native Host Dependencies

```bash
cd ../native-host
npm install
```

### Step 4: Install Extension Dependencies

```bash
cd ../extension
npm install
```

### Step 5: Setup Environment Variables

Create `.env` file in `server/`:

```env
# Server
NODE_ENV=development
PORT=8080
JWT_SECRET=your-secret-key-change-in-production

# Database (Postgres)
DATABASE_URL=postgres://user:password@localhost:5432/scoure_dev

# Or SQLite (easier for local dev)
DATABASE_URL=sqlite:./scoure.db

# S3 / Object Storage (optional for dev)
S3_ENDPOINT=http://localhost:9000
S3_ACCESS_KEY=minioadmin
S3_SECRET_KEY=minioadmin
S3_BUCKET=scoure
```

### Step 6: Setup Database

```bash
# Using SQLite (auto-created)
cd server
npm run db:init

# Or using Postgres
creatdb scoure_dev
npm run db:migrate
```

### Step 7: Build Extension

```bash
cd extension
npm run build
# Output: dist/ folder with unpacked extension
```

---

## Running Locally

### Terminal 1: Backend API

```bash
cd server
npm run dev
# API listens on http://localhost:8080
```

Output:
```
[Server] Listening on http://localhost:8080
[Database] Connected to scoure_dev
[Auth] JWT_SECRET configured
```

### Terminal 2: Native Host (optional, for plugin testing)

```bash
cd native-host
npm run dev
# Host listens on stdio + optional HTTP port 9000
```

Output:
```
[Native Host] Initialized
[Storage] Vault: ~/.scoure
[Message Handler] Ready for messages
```

### Terminal 3: Load Extension in Chrome

```bash
# 1. Open chrome://extensions
# 2. Enable "Developer mode" (top right)
# 3. Click "Load unpacked"
# 4. Select: Scoure-Joker-IDE-Guard/extension/dist
# 5. Extension is now loaded
```

---

## Testing

### Run Tests

```bash
# Backend tests
cd server
npm run test
npm run test:watch  # watch mode

# Native host tests
cd ../native-host
npm run test

# Extension tests (if available)
cd ../extension
npm run test
```

### Manual Testing Workflow

```bash
# 1. Open extension popup (Chrome icon)
#    → Should show "Setup" or "Captures" UI

# 2. Select text on any webpage
#    → Extension UI shows "Capture Selection" button

# 3. Click "Capture"
#    → Should store locally (no error)

# 4. Review in extension UI
#    → Should list captured item (metadata only)

# 5. Click "Upload"
#    → Should POST to API http://localhost:8080/v1/evidence
#    → Check backend console for receipt

# 6. Verify API stored evidence
curl http://localhost:8080/v1/evidence | jq
```

### Debug Mode

```bash
# Backend with verbose logging
DEBUG=scoure:* npm run dev

# Extension: Open chrome://extensions > Details > Errors
# Or use DevTools: Right-click extension icon > Inspect

# Native host: Check logs in ~/.scoure/logs/
```

---

## Building for Distribution

### Build Backend (Node)

```bash
cd server
npm run build
# Output: dist/ folder (transpiled JS)
```

### Build Extension

```bash
cd extension
npm run build:prod
# Output: dist/ folder (optimized, minified)
```

### Build Installer (Windows)

```bash
cd installers
# Edit install-native-host.ps1 for your paths
./install-native-host.ps1 -ExtensionId "abc123..." -HostExeSource "path/to/host.exe" -Scope User
```

---

## Antivirus & Windows Defender

### Understanding Warnings

On Windows, unsigned binaries may trigger warnings from Windows Defender or SmartScreen. This is **normal for v1 MVP**.

### Verification Steps

1. **Check code signing:**
   ```powershell
   Get-AuthenticodeSignature .\native-host.exe
   # Status: NotSigned (expected for v1)
   ```

2. **Verify hash:**
   ```powershell
   certUtil -hashfile native-host.exe SHA256
   # Compare hash with GitHub release checksum
   ```

3. **Submit to VirusTotal (optional):**
   - Visit https://www.virustotal.com
   - Upload `native-host.exe`
   - Share report link in GitHub issues

4. **Allow in Defender (temporary):**
   - Settings > Virus & threat protection > Manage settings
   - Add Scoure folder to Exclusions

### Future (v2+)

- Code signing with EV certificate (reduces false positives).
- Publish to Microsoft Store / Winget (gains reputation).
- Official build fingerprints + CI scanning.

---

## Troubleshooting

### Extension Won't Load

**Problem:** `chrome://extensions` shows error.

**Solution:**
- Check `manifest.json` syntax: `npm run validate:manifest`
- Rebuild: `npm run build`
- Reload: press Reload button in `chrome://extensions`

### Backend Won't Start

**Problem:** Port 8080 already in use.

**Solution:**
```bash
# Check process on port 8080
lsof -i :8080  # macOS/Linux
netstat -ano | findstr :8080  # Windows

# Kill process
kill -9 <PID>  # macOS/Linux
taskkill /PID <PID> /F  # Windows

# Or use different port
PORT=8081 npm run dev
```

### Database Connection Error

**Problem:** `ECONNREFUSED postgres://localhost:5432`

**Solution:**
- Check Postgres running: `psql postgres`
- Create DB: `createdb scoure_dev`
- Update `DATABASE_URL` in `.env`

### Native Host Not Found

**Problem:** Extension can't find native host.

**Solution:**
- Ensure native host exe path is correct in extension manifest
- On Windows: check registry `HKCU:\Software\Google\Chrome\NativeMessagingHosts`
- Restart Chrome completely (close all windows)

---

## Code Style & Linting

```bash
# Lint backend
cd server
npm run lint

# Fix issues
npm run lint:fix

# Format code
npm run format
```

---

## CI/CD Pipeline (GitHub Actions)

Automated checks run on each push:

```bash
npm run lint
npm run test
npm run build
```

View workflows: `.github/workflows/`

---

## Contributing to Development

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed contribution guidelines.

Quick start:
```bash
git checkout -b feat/my-feature
# Make changes
npm run test
git commit -m "feat: description"
git push origin feat/my-feature
# Open Pull Request
```
