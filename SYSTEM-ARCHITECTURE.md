AI IDEA GUARD

SYSTEM ARCHITECTURE SPECIFICATION

Version 1.0

Project: AI IDEA GUARD

Owner: JOKERVN404

Email: jokervn404@gmail.com

Website: bothelper.vn

---

1. SYSTEM OVERVIEW

AI IDEA GUARD được thiết kế như một nền tảng Digital Provenance & Evidence Platform hoạt động độc lập với mọi IDE, AI Platform và Source Repository.

Hệ thống không phụ thuộc vào bất kỳ nền tảng AI nào và có thể làm việc song song với nhiều công cụ AI khác nhau.

---

2. ARCHITECTURE OVERVIEW

                        AI IDEA GUARD

                    ┌────────────────────┐
                    │   Web Dashboard    │
                    └─────────┬──────────┘
                              │
               ┌──────────────┼──────────────┐
               │              │              │
               ▼              ▼              ▼

      Provenance       Evidence Vault    Project Manager

               │              │              │
               └───────┬──────┴──────┬───────┘
                       │             │
                       ▼             ▼

                Similarity Engine

                       │
                       ▼

              Evidence Report Engine

                       │
             ┌─────────┴──────────┐
             │                    │
             ▼                    ▼

      Browser Extension      Project Plugin

             │                    │
             └─────────┬──────────┘
                       │
                 Local Evidence API
                       │
                  PHP REST API
                       │
                 MariaDB / SQLite

---

3. SYSTEM LAYERS

Layer 1

Presentation Layer

Bao gồm

- Dashboard
- Chrome Extension
- Plugin UI
- Report Viewer

---

Layer 2

Application Layer

Bao gồm

- Session Manager
- Project Manager
- Provenance Generator
- Timeline Manager
- Report Manager

---

Layer 3

Analysis Layer

Bao gồm

- Lexical Parser
- Similarity Analyzer
- Attribution Analyzer
- Metadata Analyzer
- Timeline Analyzer

---

Layer 4

Evidence Layer

Bao gồm

- Snapshot Engine
- Hash Engine
- Signature Engine
- Evidence Chain
- Audit Logger

---

Layer 5

Storage Layer

Bao gồm

- SQLite
- MariaDB
- File Storage
- Evidence Vault

---

4. MAIN COMPONENTS

Dashboard

Nhiệm vụ

- Quản lý dự án
- Sinh Key
- Theo dõi Session
- Xem Timeline
- Sinh Report

---

Provenance Engine

Sinh

Project ID

Session ID

Evidence ID

SHA256

Timestamp

Signature

Owner Metadata

---

Project Plugin

Khi người dùng cài vào dự án.

Plugin chỉ:

- Ghi log

- Snapshot

- Hash

- Timeline

Không:

- Sửa Source

- Chỉnh Runtime

- Thay đổi Build

---

Browser Extension

Có nhiệm vụ

- Capture Prompt

- Capture Response

- Capture Metadata

- Capture Timeline

- Gửi dữ liệu về Local API khi người dùng cho phép.

---

Evidence Scanner

Có thể quét

- Source Code

- Prompt

- Markdown

- PDF

- DOCX

- Export Chat

- Git History

- ZIP

---

Similarity Engine

Các tầng phân tích

Level 1

Lexical

Level 2

Syntax

Level 3

Structure

Level 4

Architecture

Level 5

Metadata

Level 6

Timeline

Level 7

Evidence Correlation

---

5. WORKFLOW

Scenario 1

Idea Only

User

↓

Generate Provenance Key

↓

Generate Prompt

↓

Working with AI

↓

Evidence Stored

↓

Report

---

Scenario 2

Plugin Installed

Project

↓

Plugin

↓

Hash

↓

Timeline

↓

Evidence Vault

↓

Scanner

↓

Report

---

Scenario 3

Historical Analysis

Import

↓

Chat History

↓

Prompt History

↓

Source Code

↓

Compare

↓

Evidence

↓

Review Report

---

6. STORAGE

Local

SQLite

Evidence Cache

Hash Chain

Snapshots

Reports

---

Cloud

MariaDB

Authentication

Projects

Reports

Evidence Metadata

Synchronization

---

7. SECURITY MODEL

Không thay đổi

- Source

- Runtime

- Binary

- Release

Không tự động

- Upload

- Sync

- Share

- Execute

Mọi thao tác đều cần sự đồng ý của người dùng.

---

8. REPORT TYPES

Evidence Report

Similarity Report

Timeline Report

Metadata Report

Audit Report

Technical Report

---

9. OUTPUT

HTML

JSON

PDF

CSV

ZIP Evidence Package

---

10. TARGET USERS

Software Developers

AI Users

Research Teams

Content Creators

Independent Developers

Small Teams

Organizations

---

11. DESIGN OBJECTIVES

- Hoạt động độc lập.
- Không phụ thuộc nền tảng AI.
- Không ảnh hưởng dự án khách hàng.
- Có thể mở rộng bằng Plugin và Extension.
- Hỗ trợ tạo chuỗi bằng chứng kỹ thuật.
- Tôn trọng quyền riêng tư của người dùng.
- Phân tích dựa trên dữ liệu quan sát được.
- Hỗ trợ người dùng lưu trữ và trình bày bằng chứng phục vụ quá trình xem xét.

---

Copyright

© JOKERVN404

Email: jokervn404@gmail.com

Website: bothelper.vn

All Rights Reserved.
