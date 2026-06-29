# Scoure-Joker-IDE-Guard
Digital Provenance &amp; Evidence Platform  Version: 0.1.0 (Architecture 
AI IDEA GUARD

Digital Provenance & Evidence Platform

Version: 0.1.0 (Architecture Draft)

---

Overview

AI IDEA GUARD là nền tảng độc lập giúp người dùng quản lý nguồn gốc (provenance), lịch sử phát triển và bằng chứng kỹ thuật của ý tưởng, tài liệu và mã nguồn trong quá trình làm việc với các công cụ AI.

Mục tiêu của dự án là cung cấp một hệ thống ghi nhận và so sánh bằng chứng nhằm hỗ trợ người dùng xác minh quá trình phát triển của dự án thông qua các dấu thời gian, hàm băm, nhật ký và báo cáo kỹ thuật.

AI IDEA GUARD không tự động kết luận quyền sở hữu, hành vi sao chép hoặc vi phạm. Hệ thống chỉ thu thập và trình bày các bằng chứng kỹ thuật để phục vụ quá trình xem xét của con người.

---

Vision

Xây dựng một nền tảng trung lập giúp:

- Bảo tồn lịch sử hình thành ý tưởng.
- Ghi nhận provenance của dự án.
- Theo dõi quá trình phát triển.
- So sánh các phiên bản tài liệu và mã nguồn.
- Sinh báo cáo bằng chứng kỹ thuật.
- Hỗ trợ người dùng lưu trữ hồ sơ phục vụ bảo vệ quyền sở hữu trí tuệ.

---

Core Principles

- Evidence First.
- User Controlled.
- Privacy by Default.
- No Automatic Ownership Decision.
- Read-only Analysis.
- Zero Impact On Production Build.

---

Architecture

AI IDEA GUARD gồm ba nhóm chức năng chính.

1. Provenance Key Generator

Sinh định danh cho mỗi dự án hoặc phiên làm việc.

Bao gồm:

- Project ID
- Session ID
- Timestamp
- SHA-256
- Owner Metadata
- Provenance Marker

Mục đích:

- Đánh dấu nguồn gốc dự án.
- Hỗ trợ lưu trữ provenance.
- Sinh Prompt hỗ trợ người dùng khi làm việc với AI.

---

2. Project Plugin (Optional)

Plugin tùy chọn được cài đặt khi người dùng đồng ý.

Chức năng:

- Ghi nhật ký phát triển.
- Theo dõi thay đổi.
- Tính Hash.
- Ghi Timeline.
- Sinh Audit Log.

Nguyên tắc:

- Không sửa mã nguồn.
- Không sửa Build.
- Không thêm Dependency.
- Không ảnh hưởng Release.
- Không thay đổi Runtime.

Plugin hoạt động như một Sidecar Project Logger.

---

3. Evidence Scanner

Cho phép người dùng phân tích:

- Source Code
- Documentation
- Prompt History
- Chat History
- Markdown
- PDF
- Export Data

Kết quả gồm:

- Similarity Score
- Metadata Comparison
- Timeline Analysis
- Structure Comparison
- Attribution Report
- Evidence Report

---

Dashboard

Dashboard HTML là giao diện quản trị chính.

Các chức năng:

- Project Manager
- Provenance Key Generator
- Session Manager
- Timeline Viewer
- Similarity Analyzer
- Report Generator
- Evidence Vault
- Audit Viewer

---

Chrome Extension

Extension hỗ trợ:

- Capture Prompt
- Capture Response
- Capture Selected Text
- Session Marker
- Local Evidence Logging

Mọi chức năng đều yêu cầu người dùng chủ động bật.

---

Project Sidecar

Khi được cài đặt vào dự án.

.idea-guard/

manifest.json

session.db

hash_chain.log

reports/

audit/

cache/

Không được đưa vào Release Build.

---

Evidence Vault

Lưu trữ:

- SHA-256
- Timestamp
- Session
- Project
- Audit Record
- Comparison Result
- Report

Có thể triển khai:

- SQLite
- MariaDB
- PostgreSQL

---

Backend

PHP API

Các chức năng:

- Authentication
- Project
- Session
- Provenance
- Report
- Audit
- Evidence

---

Similarity Engine

Các module:

- Lexical Parser
- Structure Analyzer
- Metadata Comparator
- Timeline Analyzer
- Similarity Engine
- Attribution Analyzer

Hệ thống chỉ đánh giá các tín hiệu kỹ thuật có thể quan sát được.

---

Report Engine

Sinh báo cáo:

- HTML
- PDF
- JSON

Bao gồm:

- Timeline
- Similarity
- Hash
- Metadata
- Evidence
- Reviewer Notes

---

Security

Dự án tuân theo các nguyên tắc:

- User Consent
- Local First
- Read-only Scan
- Tamper-Evident Audit Log
- Hash Chain Verification

---

Technology Stack

Frontend

- HTML5
- CSS3
- JavaScript
- Tailwind CSS

Extension

- Chrome Extension Manifest V3

Backend

- PHP 8.x
- REST API

Database

- MariaDB
- SQLite

Evidence

- SHA-256
- Timestamp
- Digital Signature

---

Repository Structure

AI-IDEA-GUARD/

dashboard/

extension/

plugin/

scanner/

vault/

api/

docs/

reports/

README.md

LICENSE

CHANGELOG.md

---

Development Roadmap

Phase 1

- Dashboard
- Provenance Key
- Evidence Vault

Phase 2

- Chrome Extension
- Project Plugin
- Timeline

Phase 3

- Similarity Engine
- Report Engine

Phase 4

- PHP API
- Authentication
- Cloud Sync (Optional)

---

Design Goals

- Không thay đổi source code của người dùng.
- Không thay đổi build.
- Không thay đổi release artifact.
- Không tự động đưa ra kết luận pháp lý.
- Chỉ ghi nhận, lưu trữ và trình bày bằng chứng kỹ thuật.

---

License

Bản quyền, giấy phép và điều khoản sử dụng sẽ được xác định theo giấy phép do chủ sở hữu dự án lựa chọn.

Copyright Notice

AI IDEA GUARD

Digital Provenance & Evidence Platform

---

Copyright

Copyright © JOKERVN404

All rights reserved.

Project Owner

JOKERVN404

Email

jokervn404@gmail.com

Website

bothelper.vn

---

Intellectual Property

AI IDEA GUARD, including its architecture, documentation, software design, user interface concepts, provenance workflow, evidence collection workflow, similarity analysis model, project plugin architecture, dashboard design, database schema, API design, reporting workflow, and related documentation, is an original software project developed and maintained by JOKERVN404.

This repository serves as the official development repository and technical documentation for the AI IDEA GUARD project.

---

Project Purpose

AI IDEA GUARD is designed to assist users in:

- Preserving project provenance.
- Recording development history.
- Managing evidence records.
- Comparing documents and source code.
- Analyzing technical similarities.
- Generating structured evidence reports.
- Supporting intellectual property documentation and project traceability.

The software provides technical evidence and analytical reports only. It does not automatically determine ownership, infringement, or legal liability.

---

Design Principles

- Evidence First
- User Controlled
- Privacy by Default
- Read-only Analysis
- Zero Impact on Customer Projects
- Independent Evidence Collection
- Transparent Reporting

---

Ownership Statement

Unless otherwise stated, all original project architecture, technical documentation, implementation concepts, repository organization, software specifications, workflow descriptions, and original source code contained within this repository are the intellectual property of JOKERVN404.

Third-party libraries, frameworks, trademarks, and open-source components remain the property of their respective owners and are governed by their own licenses.

---

Repository Metadata

Project Name

AI IDEA GUARD

Owner

JOKERVN404

Contact

jokervn404@gmail.com

Official Website

bothelper.vn

Repository Type

Software Project

Current Status

Architecture & Development

---

Disclaimer

AI IDEA GUARD is intended to assist users by collecting, organizing, preserving, and presenting technical evidence for human review.

The software does not make legal determinations or automatically conclude ownership disputes.

Users remain responsible for complying with applicable laws, software licenses, privacy requirements, and terms of service when using this software.

---

© JOKERVN404

Email: jokervn404@gmail.com

Website: bothelper.vn

All Rights Reserved.
