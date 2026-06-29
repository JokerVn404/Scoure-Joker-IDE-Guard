AI IDEA GUARD

EVIDENCE ENGINE SPECIFICATION

Version 1.0

Project: AI IDEA GUARD

Document: 07-EVIDENCE-ENGINE.md

Owner: JOKERVN404

Email: jokervn404@gmail.com

Website: bothelper.vn

---

1. PURPOSE

Evidence Engine chịu trách nhiệm thu thập, lưu trữ và quản lý các bằng chứng kỹ thuật phát sinh trong quá trình người dùng làm việc với dự án.

Engine này không đưa ra kết luận pháp lý. Mục tiêu của nó là tạo ra một hồ sơ dữ liệu có thể kiểm chứng và truy vết.

---

2. DESIGN PRINCIPLES

- Evidence First
- Immutable Records
- Traceable
- Privacy First
- User Controlled
- Offline First
- Read-only Collection

---

3. EVIDENCE TYPES

Hệ thống hỗ trợ các loại bằng chứng sau:

Prompt
Response
Source Code Snapshot
Documentation
Markdown
PDF
Image
Screenshot
Timeline Event
Metadata Record
Project Marker
Hash Record
Report

---

4. EVIDENCE OBJECT

Mỗi bằng chứng bao gồm:

Evidence UUID
Project UUID
Session UUID
Evidence Type
Created Time
SHA-256
Source
Status

---

5. SOURCE TYPES

Dashboard
Desktop App
Browser Extension
Project Sidecar
Manual Import
Scanner
API

---

6. HASHING

Mỗi Evidence sinh:

SHA-256

Content Length

Timestamp

Hash dùng để kiểm tra tính toàn vẹn của dữ liệu.

---

7. SNAPSHOT

Snapshot ghi nhận trạng thái của dữ liệu tại thời điểm thu thập.

Có thể áp dụng cho:

- Source Code
- Prompt
- Response
- Document
- Report

---

8. TIMELINE LINK

Mỗi Evidence liên kết tới Timeline Event tương ứng.

Ví dụ:

Evidence

↓

Timeline Event

↓

Session

↓

Project

---

9. FILE SUPPORT

Định dạng hỗ trợ:

TXT
MD
HTML
PDF
DOCX
JSON
CSV
ZIP
PNG
JPG

---

10. IMPORT MODE

Nguồn nhập:

- Manual Import
- Drag & Drop
- Folder Scan
- Browser Extension
- Project Plugin
- API Upload

---

11. EXPORT MODE

Cho phép xuất:

JSON
HTML
PDF
ZIP

---

12. EVIDENCE STATUS

Collected
Verified
Archived
Exported
Deleted

---

13. RETENTION

Theo mặc định:

- Evidence thuộc quyền kiểm soát của người dùng.
- Không tự động đồng bộ.
- Có thể sao lưu.
- Có thể xóa.

---

14. INTEGRITY CHECK

Quy trình kiểm tra:

Load Evidence

↓

Verify Hash

↓

Verify Metadata

↓

Verify Timeline

↓

Integrity Result

---

15. CHAIN OF EVIDENCE

Mỗi Evidence có thể liên kết với:

- Prompt
- Response
- Timeline
- Session
- Report

để tạo thành chuỗi dữ liệu có thể truy vết.

---

16. STORAGE

Hỗ trợ:

SQLite
MariaDB
PostgreSQL

---

17. SECURITY

Evidence Engine:

- Không sửa nội dung bằng chứng.
- Không tự động phân tích ngoài yêu cầu của người dùng.
- Không chia sẻ dữ liệu nếu chưa được phép.
- Chỉ hoạt động trên dữ liệu mà người dùng cung cấp hoặc cho phép truy cập.

---

18. FUTURE EXTENSIONS

Có thể mở rộng:

- Digital Signature
- Merkle Tree
- External Timestamp
- Multi-Device Sync
- Evidence Encryption

---

19. LIMITATIONS

Evidence Engine không:

- Xác định quyền sở hữu trí tuệ.
- Kết luận rằng một hệ thống đã sao chép nội dung.
- Thay thế đánh giá của con người hoặc cơ quan có thẩm quyền.

Nó cung cấp dữ liệu, dấu thời gian và các bản ghi phục vụ việc xem xét.

---

20. COPYRIGHT

© JOKERVN404

Email: jokervn404@gmail.com

Website: bothelper.vn

All Rights Reserved.
