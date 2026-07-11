AI IDEA GUARD

DATABASE DESIGN SPECIFICATION

Version 1.0

Project: AI IDEA GUARD

Document: 03-DATABASE-DESIGN.md

Owner: JOKERVN404

Email: jokervn404@gmail.com

Website: bothelper.vn
# Scoure Joker IDE Guard

> AI-powered Code Provenance & Evidence Tracking System

---

## 🚀 Overview

Scoure Joker IDE Guard là hệ thống giúp:
- Truy vết nguồn gốc code (Provenance)
- Phát hiện copy / AI-generated code
- Tạo bằng chứng kỹ thuật (Evidence)
- Bảo vệ bản quyền developer

---

## 🎯 Problem

- Code bị copy nhưng không có bằng chứng
- AI code khó phân biệt nguồn gốc
- Không có hệ thống audit timeline

---

## 💡 Solution

- Provenance Engine → ghi lại lịch sử code
- Evidence Engine → tạo bằng chứng pháp lý
- Similarity Engine → phát hiện trùng lặp
- Dashboard → visualize toàn bộ hệ thống

---

## 🏗 Architecture


User (IDE / Extension)
↓
Collector → Provenance Engine
↓
Similarity Engine → Evidence Engine
↓
API (PHP)
↓
Database
↓
Dashboard


---

## ⚙️ Tech Stack

- Backend: PHP (REST API)
- Database: MySQL
- Extension: Chrome / IDE Plugin
- AI: Code Similarity Engine

---

## 📦 Features

- Code tracking theo thời gian
- Snapshot & hash verification
- AI similarity detection
- Evidence export (PDF / JSON)

---

## 🤝 Contributing

Xem `CONTRIBUTING.md`

---

## 📜 License

MIT License
