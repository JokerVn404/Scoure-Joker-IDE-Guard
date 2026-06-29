AI IDEA GUARD

PROVENANCE ENGINE SPECIFICATION

Version 1.0

Project: AI IDEA GUARD

Document: 06-PROVENANCE-ENGINE.md

Owner: JOKERVN404

Email: jokervn404@gmail.com

Website: bothelper.vn

---

1. PURPOSE

Provenance Engine là thành phần chịu trách nhiệm ghi nhận nguồn gốc dữ liệu (data provenance) trong phạm vi dự án AI IDEA GUARD.

Mục tiêu của thành phần này là:

- Gắn định danh cho phiên làm việc.
- Liên kết các bản ghi với Project và Session.
- Duy trì chuỗi bằng chứng (Evidence Chain).
- Cho phép kiểm tra tính toàn vẹn của dữ liệu.
- Hỗ trợ người dùng quản lý lịch sử phát triển dự án.

Engine này không tự động kết luận về quyền sở hữu trí tuệ hay hành vi sao chép, mà chỉ tạo và quản lý các bản ghi phục vụ việc kiểm chứng.

---

2. DESIGN GOALS

- Deterministic
- Traceable
- Tamper-Evident
- Privacy First
- User Controlled
- Offline First
- Cross Platform

---

3. CORE COMPONENTS

Project

↓

Session

↓

Provenance Key

↓

Prompt

↓

Response

↓

Evidence

↓

Timeline

↓

Report

---

4. PROJECT IDENTITY

Mỗi Project sinh:

Project UUID

Created Time

Owner ID

Project Hash

Project UUID không thay đổi trong suốt vòng đời dự án.

---

5. SESSION IDENTITY

Mỗi Session sinh:

Session UUID

Start Time

End Time

Client Type

Client Version

Ví dụ:

Dashboard

Plugin

Browser Extension

Scanner

---

6. PROVENANCE KEY

Mỗi phiên có thể tạo một Provenance Key.

Ví dụ:

AIIG-2026-XXXXXXXX

Key được liên kết với:

- Project
- Session
- Timestamp
- Hash

---

7. PROJECT MARKER

Marker là chuỗi nhận diện do người dùng cấu hình.

Ví dụ:

[AI-IDEA-GUARD:SIG:v1]

hoặc

[PROJECT-MARKER]

Marker chỉ đóng vai trò nhận diện dự án và không ảnh hưởng đến chức năng của mã nguồn.

---

8. PROMPT RECORD

Mỗi Prompt được lưu với:

Prompt UUID

SHA-256

Timestamp

Session UUID

---

9. RESPONSE RECORD

Mỗi phản hồi được lưu với:

Response UUID

Provider

Model

SHA-256

Timestamp

---

10. HASH CHAIN

Mỗi bản ghi tham chiếu tới bản ghi trước.

Record A

↓

Record B

↓

Record C

↓

Record D

Việc này giúp phát hiện thay đổi trái phép trong chuỗi dữ liệu.

---

11. TIMELINE ENGINE

Timeline ghi nhận các sự kiện như:

Project Created

Session Started

Prompt Saved

Response Saved

Evidence Added

Report Generated

---

12. EVIDENCE LINK

Một Evidence có thể tham chiếu:

Prompt

Response

Document

Source Snapshot

Screenshot

Timeline Event

---

13. SNAPSHOT

Snapshot là ảnh chụp trạng thái của dữ liệu tại một thời điểm.

Có thể áp dụng cho:

- Source
- Document
- Prompt
- Response
- Report

---

14. SIGNATURE

Mỗi đối tượng có thể lưu:

SHA-256

Optional Signature

Timestamp

Trong phiên bản đầu, chữ ký số là tùy chọn.

---

15. VERIFY PROCESS

Quy trình kiểm tra:

Load Record

↓

Verify Hash

↓

Verify Timeline

↓

Verify References

↓

Generate Result

---

16. EXPORT FORMAT

Engine hỗ trợ:

JSON

HTML

PDF

ZIP

---

17. STORAGE MODE

Hỗ trợ:

SQLite

MariaDB

PostgreSQL

---

18. OFFLINE MODE

Engine hoạt động hoàn toàn ngoại tuyến.

Nếu người dùng không bật đồng bộ:

- Không gửi dữ liệu lên máy chủ.
- Không chia sẻ dữ liệu.
- Không truyền Prompt hoặc Response ra ngoài.

---

19. ONLINE MODE

Nếu được người dùng cho phép:

- Đồng bộ Timeline.
- Đồng bộ Evidence.
- Đồng bộ Report.
- Sao lưu dữ liệu.

---

20. PRIVACY PRINCIPLES

Engine không:

- Thu thập dữ liệu ngoài phạm vi người dùng cho phép.
- Đọc dự án khi chưa được cấp quyền.
- Tự động tải dữ liệu lên máy chủ.
- Tự động gửi báo cáo.

---

21. EXTENSIBILITY

Trong các phiên bản sau có thể bổ sung:

- Merkle Tree cho chuỗi băm.
- Chữ ký số.
- Time-stamping từ bên thứ ba.
- Hỗ trợ nhiều nhà cung cấp AI.
- Đồng bộ đa thiết bị.

Các tính năng này được thiết kế như tùy chọn, không bắt buộc.

---

22. LIMITATIONS

Provenance Engine:

- Không xác định quyền sở hữu trí tuệ.
- Không chứng minh độc lập việc một ý tưởng bị sao chép.
- Không kết luận hành vi của bất kỳ hệ thống AI nào.

Vai trò của Engine là ghi nhận và quản lý dữ liệu phục vụ việc phân tích và kiểm chứng sau này.

---

23. COPYRIGHT

© JOKERVN404

Email: jokervn404@gmail.com

Website: bothelper.vn

All Rights Reserved.
