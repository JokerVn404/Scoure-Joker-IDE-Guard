AI IDEA GUARD

DASHBOARD SPECIFICATION

Version 1.0

Project: AI IDEA GUARD

Document: 05-DASHBOARD-SPECIFICATION.md

Owner: JOKERVN404

Email: jokervn404@gmail.com

Website: bothelper.vn

---

1. PURPOSE

Dashboard là trung tâm điều khiển của AI IDEA GUARD.

Toàn bộ Plugin, Extension, Scanner và API đều kết nối về Dashboard.

Dashboard không chỉ là giao diện hiển thị mà còn là trung tâm phân tích, quản lý bằng chứng và điều phối các phiên làm việc.

---

2. DESIGN PRINCIPLES

Dashboard phải:

- Hoạt động nhanh.
- Giao diện rõ ràng.
- Hỗ trợ Desktop và Mobile.
- Không phụ thuộc AI Provider.
- Có thể mở rộng bằng Module.
- Hỗ trợ Dark Mode mặc định.

---

3. MAIN MODULES

Dashboard Home

Hiển thị:

- Tổng số Project
- Session đang hoạt động
- Plugin Online
- Extension Online
- Scanner Status
- API Status
- Recent Reports
- Timeline

---

Project Manager

Quản lý:

- Project
- Folder
- Owner
- Metadata
- Session
- Provenance

---

Provenance Center

Chức năng:

- Generate Project Key
- Generate Session Key
- Generate Prompt
- Export Metadata
- Verify Marker

---

Session Manager

Quản lý:

- Active Sessions
- Completed Sessions
- Session Timeline
- Session Hash
- Session Report

---

Evidence Vault

Hiển thị:

- Prompt
- Response
- Source Snapshot
- Document Snapshot
- Timeline
- Screenshots
- Reports

---

Similarity Center

Phân tích:

- Text
- Source Code
- Prompt
- Documentation
- Metadata
- Timeline

---

Report Center

Quản lý:

- HTML Report
- PDF Report
- JSON Report
- ZIP Evidence Package

---

API Center

Hiển thị:

- API Status
- API Token
- Upload Queue
- Sync Queue
- Error Log

---

Plugin Center

Quản lý:

- Installed Plugins
- Plugin Version
- Plugin Status
- Plugin Timeline

---

Browser Extension Center

Hiển thị:

- Connected Browser
- Session Capture
- Prompt Capture
- Response Capture
- Browser History Import

---

Settings

Bao gồm:

General

Security

Privacy

Storage

Evidence

API

Extension

Plugin

Account

---

4. SIDEBAR MENU

Dashboard

Projects

Sessions

Provenance

Evidence

Similarity

Reports

Timeline

Plugin

Extension

API

Settings

---

5. HEADER

Header hiển thị:

- Current Project
- Current Session
- Search
- Notifications
- User Profile

---

6. PROJECT PAGE

Hiển thị:

Tên Project

Ngày tạo

Owner

Metadata

Session

Hash

Status

Evidence Count

Report Count

---

7. SESSION PAGE

Hiển thị:

Session ID

Start Time

End Time

Duration

Evidence

Timeline

Prompt Count

Response Count

---

8. PROVENANCE PAGE

Các chức năng:

Generate Provenance Key

Generate Prompt

Export Marker

Verify Marker

History

Hash

Signature

---

9. SCANNER PAGE

Cho phép:

Import Folder

Import Source

Import Prompt

Import Chat History

Import Documentation

Import ZIP

Import PDF

Import Markdown

---

10. SCAN RESULT

Hiển thị:

Similarity Score

Metadata Status

Timeline Analysis

Evidence Summary

Review Priority

Findings

---

11. REPORT PAGE

Xuất:

HTML

PDF

JSON

CSV

ZIP

---

12. TIMELINE PAGE

Hiển thị theo dạng Timeline:

Project Created

Session Started

Prompt Saved

Response Saved

Evidence Created

Report Generated

Scan Completed

---

13. LIVE MONITOR

Nếu người dùng bật:

Dashboard hiển thị:

Plugin Online

Extension Online

Current Session

Evidence Count

Current Timeline

Latest Prompt

Latest Response

Latest Event

---

14. NOTIFICATION CENTER

Thông báo:

Evidence Created

Metadata Changed

High Similarity

Marker Missing

Plugin Offline

API Error

Report Ready

---

15. SEARCH

Tìm kiếm theo:

Project

Session

Prompt

Evidence

Hash

Report

Timeline

---

16. FILTER

Lọc theo:

Date

Project

Provider

Similarity Score

Evidence Type

Review Status

---

17. EXPORT

Dashboard hỗ trợ:

Export Project

Export Evidence

Export Report

Export Timeline

Export Database

Backup Vault

---

18. SECURITY

Dashboard không:

- Tự sửa Source.
- Tự Build.
- Tự Upload.
- Tự Share dữ liệu.
- Tự đồng bộ Cloud nếu chưa được bật.

Mọi thao tác đều yêu cầu sự đồng ý của người dùng.

---

19. UI STYLE

Theme:

Cyber Dark

Primary:

#22D3EE

Accent:

#8B5CF6

Success:

#22C55E

Warning:

#F59E0B

Danger:

#EF4444

Background:

#070B14

---

20. FUTURE MODULES

Planned:

AI Assistant

Evidence Explorer

Graph Analysis

Timeline Visualization

Project Diff

Multi-Project Comparison

Organization Dashboard

Enterprise Console

---

21. COPYRIGHT

© JOKERVN404

Email: jokervn404@gmail.com

Website: bothelper.vn

All Rights Reserved.
