---
globs: "**/controllers/**, **/routes/**, **/api/**, **/middleware/**"
---

# 🌐 Rule: API Conventions

> Quy tắc thiết kế API chuẩn RESTful.

## URL Design

```
# Format: /api/v[N]/[resource-plural]
# Dùng nouns, KHÔNG dùng verbs

✅ GET  /api/v1/users
✅ POST /api/v1/users
✅ GET  /api/v1/users/123
✅ PATCH /api/v1/users/123

❌ GET  /api/v1/getUsers
❌ POST /api/v1/createUser
❌ GET  /api/v1/user/123        # phải plural
```

## HTTP Methods

| Method | Mục đích | Idempotent | Body |
|---|---|---|---|
| GET | Đọc resource | ✅ | Không |
| POST | Tạo resource | ❌ | Có |
| PUT | Replace toàn bộ | ✅ | Có |
| PATCH | Update một phần | ❌ | Có |
| DELETE | Xóa resource | ✅ | Không |

## Response Envelope

```json
// Success response
{
  "success": true,
  "data": { ... },
  "meta": {
    "page": 1,
    "limit": 20,
    "total": 150,
    "totalPages": 8
  }
}

// Error response
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Dữ liệu không hợp lệ",
    "details": [
      { "field": "email", "message": "Email không đúng định dạng" }
    ]
  }
}
```

## Pagination

```
# Cursor-based (recommended cho large datasets)
GET /api/v1/posts?cursor=abc123&limit=20

# Offset-based (simpler, cho small datasets)
GET /api/v1/users?page=2&limit=20
```

## Filtering & Sorting

```
GET /api/v1/products?category=electronics&price_min=100&price_max=500
GET /api/v1/users?sort=-created_at,name    # - prefix = DESC
GET /api/v1/posts?search=typescript&status=published
```

## Versioning

```
# URL versioning (recommended)
/api/v1/users
/api/v2/users

# Header versioning (alternative)
Accept: application/vnd.myapp.v1+json
```

## Rate Limiting Headers

```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1640000000
Retry-After: 60
```

## Rules

1. Luôn return JSON, kể cả errors
2. Dùng HTTP status codes đúng ngữ nghĩa
3. Pagination bắt buộc cho list endpoints
4. Validate input ở API layer
5. Version API từ ngày đầu tiên
6. CORS config rõ ràng
7. Rate limiting cho public APIs
8. API documentation (OpenAPI/Swagger) luôn up-to-date
