AI IDEA GUARD

PHP API SPECIFICATION

Version 1.0

Project: AI IDEA GUARD
Document: 04-PHP-API-SPECIFICATION.md
Owner: JOKERVN404
Email: jokervn404@gmail.com
Website: bothelper.vn

---

1. API PURPOSE

PHP API là tầng kết nối giữa Dashboard, Plugin, Chrome Extension, Scanner và Database.

API chịu trách nhiệm:

- Quản lý tài khoản
- Quản lý Project
- Quản lý Session
- Sinh Provenance Key
- Nhận Evidence Record
- Lưu Hash
- Lưu Timeline
- Tạo Report
- Đồng bộ dữ liệu khi người dùng cho phép

---

2. API PRINCIPLES

- User Consent First
- Read-only Evidence Intake
- No Source Modification
- No Automatic Legal Conclusion
- Privacy by Default
- Hash Before Store
- Tamper-Evident Logs
- Exportable Reports

---

3. BASE URL

https://bothelper.vn/ai-idea-guard/api/

Development:

http://localhost/ai-idea-guard/api/

---

4. API VERSIONING

/api/v1/

Example:

POST /api/v1/projects/create

---

5. AUTHENTICATION

API sử dụng Token Authentication.

Headers

Authorization: Bearer <api_token>
Content-Type: application/json

Token Types

user_token
project_token
plugin_token
extension_token
scanner_token

---

6. STANDARD RESPONSE FORMAT

Success

{
  "ok": true,
  "data": {},
  "message": "success",
  "timestamp": "2026-06-29T00:00:00Z"
}

Error

{
  "ok": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input"
  },
  "timestamp": "2026-06-29T00:00:00Z"
}

---

7. USER API

Create User

POST /api/v1/users/create

Request:

{
  "email": "user@example.com",
  "display_name": "User Name",
  "website": "example.com"
}

Response:

{
  "ok": true,
  "data": {
    "user_id": "uuid",
    "api_token": "token"
  }
}

---

Get User Profile

GET /api/v1/users/me

---

8. PROJECT API

Create Project

POST /api/v1/projects/create

Request:

{
  "project_name": "My AI Project",
  "description": "Project description",
  "project_type": "software"
}

Response:

{
  "ok": true,
  "data": {
    "project_id": "uuid"
  }
}

---

List Projects

GET /api/v1/projects

---

Get Project

GET /api/v1/projects/{project_id}

---

Update Project

POST /api/v1/projects/{project_id}/update

---

9. SESSION API

Start Session

POST /api/v1/sessions/start

Request:

{
  "project_id": "uuid",
  "client_type": "dashboard | plugin | extension | scanner",
  "client_version": "0.1.0"
}

Response:

{
  "ok": true,
  "data": {
    "session_id": "uuid",
    "started_at": "2026-06-29T00:00:00Z"
  }
}

---

End Session

POST /api/v1/sessions/{session_id}/end

---

10. PROVENANCE KEY API

Generate Provenance Key

POST /api/v1/provenance/generate

Request:

{
  "project_id": "uuid",
  "session_id": "uuid",
  "owner_marker": "JOKERVN404",
  "email": "jokervn404@gmail.com",
  "website": "bothelper.vn"
}

Response:

{
  "ok": true,
  "data": {
    "provenance_key": "AIIG-20260629-XXXX",
    "marker": "[AI-IDEA-GUARD:SIG:v1:AIIG-20260629-XXXX]",
    "sha256": "hash",
    "prompt": "Generated prompt text"
  }
}

---

11. PROMPT API

Save Prompt

POST /api/v1/prompts/save

Request:

{
  "project_id": "uuid",
  "session_id": "uuid",
  "content": "prompt content",
  "source": "manual | extension | plugin"
}

---

Save Response

POST /api/v1/responses/save

Request:

{
  "project_id": "uuid",
  "session_id": "uuid",
  "prompt_id": "uuid",
  "provider": "openai | gemini | claude | other",
  "model": "model-name",
  "content": "response content"
}

---

12. EVIDENCE API

Create Evidence Record

POST /api/v1/evidence/create

Request:

{
  "project_id": "uuid",
  "session_id": "uuid",
  "evidence_type": "prompt | response | source | document | screenshot | report",
  "content_sha256": "hash",
  "metadata": {}
}

---

Upload Evidence Attachment

POST /api/v1/evidence/upload

Content-Type:

multipart/form-data

Fields:

project_id
session_id
evidence_type
file

---

Get Evidence Record

GET /api/v1/evidence/{evidence_id}

---

13. SCAN API

Compare Content

POST /api/v1/scan/compare

Request:

{
  "project_id": "uuid",
  "source_text": "original content",
  "target_text": "compared content",
  "scan_type": "text | source | metadata | mixed"
}

Response:

{
  "ok": true,
  "data": {
    "similarity_score": 0.91,
    "metadata_status": "missing | preserved | changed | unknown",
    "review_priority": "low | medium | high",
    "findings": []
  }
}

---

14. REPORT API

Generate Report

POST /api/v1/reports/generate

Request:

{
  "project_id": "uuid",
  "report_type": "evidence | similarity | timeline | metadata | full",
  "evidence_ids": []
}

Response:

{
  "ok": true,
  "data": {
    "report_id": "uuid",
    "html_url": "reports/report.html",
    "json_url": "reports/report.json",
    "sha256": "hash"
  }
}

---

Get Report

GET /api/v1/reports/{report_id}

---

Export Report

GET /api/v1/reports/{report_id}/export?format=pdf

Supported formats:

html
json
pdf
zip

---

15. TIMELINE API

Add Timeline Event

POST /api/v1/timeline/add

Request:

{
  "project_id": "uuid",
  "session_id": "uuid",
  "event_type": "project_created | prompt_saved | response_saved | evidence_created | scan_completed | report_generated",
  "description": "Event description",
  "event_hash": "hash"
}

---

Get Project Timeline

GET /api/v1/timeline/{project_id}

---

16. PLUGIN API

Register Plugin

POST /api/v1/plugin/register

Request:

{
  "project_id": "uuid",
  "plugin_type": "project-sidecar",
  "plugin_version": "0.1.0",
  "environment": "windows | linux | macos"
}

---

Submit Plugin Log

POST /api/v1/plugin/log

Request:

{
  "project_id": "uuid",
  "session_id": "uuid",
  "level": "info | warning | error",
  "message": "log message",
  "hash": "hash"
}

---

17. EXTENSION API

Register Extension

POST /api/v1/extension/register

---

Submit Captured Session

POST /api/v1/extension/capture

Request:

{
  "project_id": "uuid",
  "session_id": "uuid",
  "page_url_hash": "hash",
  "captured_type": "prompt | response | selected_text",
  "content": "captured content"
}

---

18. SECURITY REQUIREMENTS

- API phải kiểm tra token.
- Mọi input phải validate.
- File upload phải giới hạn loại file.
- Không cho upload executable mặc định.
- Tất cả record quan trọng phải có SHA-256.
- Không trả dữ liệu project nếu token không có quyền.
- Không log plaintext secret.
- Không tự động đồng bộ dữ liệu nếu người dùng chưa bật.

---

19. RATE LIMIT

Default:

60 requests / minute / token

Upload:

20 requests / minute / token

Report generation:

10 requests / minute / token

---

20. ERROR CODES

AUTH_REQUIRED
TOKEN_INVALID
PERMISSION_DENIED
VALIDATION_ERROR
PROJECT_NOT_FOUND
SESSION_NOT_FOUND
EVIDENCE_NOT_FOUND
REPORT_NOT_FOUND
UPLOAD_BLOCKED
RATE_LIMITED
SERVER_ERROR

---

21. DEPLOYMENT TARGET

Target:

cPanel PHP Hosting
PHP 8.x
MariaDB
Apache / LiteSpeed
HTTPS

---

22. NON-GOALS

API không được:

- Tự kết luận vi phạm bản quyền.
- Tự sửa source code người dùng.
- Tự động upload dữ liệu riêng tư.
- Chạy scan trái phép.
- Can thiệp build/release của khách hàng.

---

23. COPYRIGHT

© JOKERVN404
Email: jokervn404@gmail.com
Website: bothelper.vn

All Rights Reserved.
