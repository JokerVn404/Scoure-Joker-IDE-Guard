AI IDEA GUARD

DATABASE DESIGN SPECIFICATION

Version 1.0

Project: AI IDEA GUARD

Document: 03-DATABASE-DESIGN.md

Owner: JOKERVN404

Email: jokervn404@gmail.com

Website: bothelper.vn
# Database Design

## Tables

### users
| Field | Type |
|------|------|
| id | INT |
| email | VARCHAR |
| created_at | TIMESTAMP |

---

### projects
| Field | Type |
|------|------|
| id | INT |
| user_id | INT |
| name | VARCHAR |

---

### code_snapshots
| Field | Type |
|------|------|
| id | INT |
| project_id | INT |
| file_path | TEXT |
| hash | VARCHAR |
| content | TEXT |
| created_at | TIMESTAMP |

---

### provenance_logs
| Field | Type |
|------|------|
| id | INT |
| snapshot_id | INT |
| action | VARCHAR |
| timestamp | TIMESTAMP |

---

### evidence_reports
| Field | Type |
|------|------|
| id | INT |
| project_id | INT |
| report_json | JSON |
| created_at | TIMESTAMP |
