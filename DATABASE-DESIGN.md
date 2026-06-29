AI IDEA GUARD

DATABASE DESIGN SPECIFICATION

Version 1.0

Project: AI IDEA GUARD

Document: 03-DATABASE-DESIGN.md

Owner: JOKERVN404

Email: jokervn404@gmail.com

Website: bothelper.vn

---

1. DATABASE OBJECTIVES

Cơ sở dữ liệu của AI IDEA GUARD được thiết kế để quản lý toàn bộ vòng đời của một dự án, từ giai đoạn hình thành ý tưởng cho đến khi hoàn thiện sản phẩm.

Hệ thống ưu tiên:

- Digital Provenance
- Timeline
- Evidence Chain
- Similarity Analysis
- Technical Audit
- Privacy First

Mọi dữ liệu đều được tổ chức theo hướng có thể truy vết (Traceable) và kiểm chứng (Verifiable).

---

2. DATABASE ARCHITECTURE

User
 │
 ├── Projects
 │      │
 │      ├── Sessions
 │      │      │
 │      │      ├── Prompt History
 │      │      ├── Response History
 │      │      ├── Evidence
 │      │      ├── Timeline
 │      │      ├── Metadata
 │      │      └── Reports
 │      │
 │      └── Provenance Key
 │
 └── Audit

---

3. MAIN TABLES

users

Thông tin tài khoản.

id

uuid

email

display_name

website

created_at

updated_at

---

projects

Quản lý dự án.

id

uuid

user_id

project_name

description

project_type

created_at

updated_at

---

project_sessions

Mỗi lần làm việc.

id

session_uuid

project_id

start_time

end_time

status

client_version

---

provenance_keys

Lưu Provenance Key.

id

project_id

session_id

key_version

marker

sha256

signature

created_at

---

prompts

Prompt người dùng.

id

session_id

sequence

content

sha256

created_at

---

responses

Kết quả AI.

id

prompt_id

provider

model

content

sha256

created_at

---

evidence_records

Chuỗi bằng chứng.

id

project_id

session_id

evidence_type

hash

signature

created_at

---

source_snapshots

Snapshot mã nguồn.

id

project_id

file_path

sha256

size

captured_at

---

document_snapshots

Snapshot tài liệu.

id

project_id

document_type

hash

captured_at

---

metadata_records

Metadata dự án.

id

project_id

author

email

website

marker

created_at

---

similarity_reports

Kết quả so sánh.

id

project_id

score

engine_version

generated_at

---

similarity_details

Chi tiết từng phát hiện.

id

report_id

category

confidence

description

location

evidence_reference

---

timeline_events

Timeline.

id

project_id

event_type

description

timestamp

---

audit_logs

Nhật ký.

id

project_id

level

module

message

timestamp

---

attachments

Tệp đính kèm.

id

project_id

type

filename

sha256

storage_path

---

generated_reports

Báo cáo.

id

project_id

report_type

filename

sha256

created_at

---

4. FUTURE TABLES

Reserved.

plugin_logs

extension_logs

browser_sessions

api_requests

api_tokens

notifications

review_notes

review_status

report_exports

organization

team

permissions

license

payment

activity

devices

---

5. DATABASE RELATIONSHIP

User

↓

Projects

↓

Sessions

↓

Prompt

↓

Response

↓

Evidence

↓

Similarity

↓

Report

---

6. STORAGE STRATEGY

Local

SQLite

Cloud

MariaDB

Future

PostgreSQL

---

7. HASH STRATEGY

Mỗi đối tượng sinh:

- SHA256
- UUID
- Timestamp

Tùy chọn:

- Digital Signature

---

8. EVIDENCE CHAIN

Prompt

↓

Hash

↓

Response

↓

Hash

↓

Evidence

↓

Report

Mỗi record đều có thể truy vết ngược.

---

9. DATA RETENTION

Theo mặc định:

- Người dùng sở hữu dữ liệu.
- Không đồng bộ lên Cloud nếu chưa bật.
- Có thể xuất toàn bộ dữ liệu.
- Có thể xóa toàn bộ dữ liệu.

---

10. DESIGN PRINCIPLES

- Local First
- Privacy First
- User Controlled
- Evidence Based
- Immutable History (đối với bản ghi đã ký)
- Read-only Analysis
- Zero Impact On Customer Projects

---

11. VERSIONING

Database sử dụng Schema Version.

Ví dụ:

Schema 1.0

Schema 1.1

Schema 2.0

Cho phép Migration tự động.

---

12. FUTURE EXPANSION

Database được thiết kế để mở rộng cho:

- Desktop Application
- Chrome Extension
- Visual Studio Extension
- VS Code Extension
- JetBrains Plugin
- AI Plugin
- Web Dashboard
- REST API
- Mobile Application

Mọi thành phần đều sử dụng chung một mô hình dữ liệu nhằm đảm bảo tính nhất quán giữa Dashboard, Plugin và Scanner.

---

Copyright

© JOKERVN404

Email: jokervn404@gmail.com

Website: bothelper.vn

All Rights Reserved.
