# API Specification — v0.1.0 MVP

Base URL: `http://localhost:8080` (dev), `https://api.scoure.example.com` (prod).

---

## Authentication

All endpoints require Bearer token (JWT) or API key header.

```bash
# JWT (user login)
curl -H "Authorization: Bearer <jwt_token>" http://localhost:8080/v1/evidence

# API Key (agent / plugin)
curl -H "X-Api-Key: <api_key>" http://localhost:8080/v1/evidence
```

---

## Endpoints

### 1. Auth / Login

**POST /auth/login**

Request:
```json
{ "username": "user@example.com", "password": "..." }
```

Response:
```json
{
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGc...",
  "token_type": "Bearer",
  "expires_in": 3600
}
```

---

### 2. Projects

**POST /v1/projects** — Create a project

Request:
```json
{
  "name": "My Project",
  "description": "Optional description"
}
```

Response:
```json
{
  "id": "550e8400-e29b-41d4-a716-446655440000",
  "name": "My Project",
  "owner_id": "user123",
  "created_at": "2024-01-01T12:00:00Z"
}
```

**GET /v1/projects** — List projects

Response:
```json
[
  {
    "id": "550e8400-...",
    "name": "My Project",
    "created_at": "2024-01-01T12:00:00Z"
  }
]
```

---

### 3. Evidence

**POST /v1/evidence** — Upload evidence unit

Headers:
```
Content-Type: multipart/form-data
Authorization: Bearer <token>
```

Request (multipart):
```
--boundary
Content-Disposition: form-data; name="metadata"
Content-Type: application/json

{
  "project_id": "550e8400-...",
  "type": "file",
  "content_hash": "sha256:abcd1234...",
  "consent_id": "consent-uuid-...",
  "metadata": {
    "path": "/src/main.py",
    "timestamp": "2024-01-01T12:00:00Z"
  }
}
--boundary
Content-Disposition: form-data; name="file"; filename="main.py"
Content-Type: application/octet-stream

<binary file content>
--boundary--
```

Response:
```json
{
  "id": "evidence-uuid-...",
  "stored": true,
  "signed": true,
  "created_at": "2024-01-01T12:00:00Z"
}
```

**GET /v1/evidence/{id}** — Retrieve evidence metadata

Response:
```json
{
  "id": "evidence-uuid-...",
  "project_id": "550e8400-...",
  "type": "file",
  "content_hash": "sha256:abcd1234...",
  "metadata": {
    "path": "/src/main.py",
    "timestamp": "2024-01-01T12:00:00Z"
  },
  "signatures": [
    {
      "method": "sha256",
      "value": "sig-value-...",
      "signed_by": "core",
      "key_id": "key-1"
    }
  ],
  "created_at": "2024-01-01T12:00:00Z"
}
```

---

### 4. Plugins / Registration

**POST /v1/projects/{projectId}/plugins/register** — Register plugin + consent

Request:
```json
{
  "plugin_id": "com.scoure.local",
  "plugin_version": "0.1.0",
  "user_id": "user123",
  "consent_id": "consent-uuid-..."
}
```

Response:
```json
{
  "plugin_id": "com.scoure.local",
  "registered_at": "2024-01-01T12:00:00Z"
}
```

**POST /v1/plugins/{pluginId}/heartbeat** — Plugin heartbeat (opt-in)

Request:
```json
{
  "timestamp": "2024-01-01T12:00:00Z"
}
```

Response:
```json
{
  "last_seen": "2024-01-01T12:00:00Z"
}
```

---

### 5. Error Responses

All errors follow this format:

```json
{
  "error": "INVALID_REQUEST",
  "message": "Consent ID not found",
  "details": { ... }
}
```

Common status codes:
- `200` OK
- `201` Created
- `400` Bad Request
- `401` Unauthorized
- `403` Forbidden (consent not valid)
- `404` Not Found
- `500` Server Error

---

## Rate Limiting (v1)

- 100 requests per minute per user/API key.
- Header: `X-RateLimit-Remaining`.

---

## Pagination (v1)

Query params:
- `page` — page number (default: 1).
- `per_page` — items per page (default: 30, max: 100).

Response:
```json
{
  "data": [...],
  "page": 1,
  "per_page": 30,
  "total": 150
}
```
