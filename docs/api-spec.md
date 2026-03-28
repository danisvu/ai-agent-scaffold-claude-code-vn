# 📡 API Specification

> Template mô tả API endpoints — cập nhật khi thêm/sửa API.

## Base URL

```
Development: http://localhost:3000/api/v1
Staging:     https://staging.app.com/api/v1
Production:  https://app.com/api/v1
```

## Authentication

```
Authorization: Bearer <jwt_access_token>
```

## Common Response Format

### Success
```json
{
  "success": true,
  "data": { ... },
  "meta": { "page": 1, "limit": 20, "total": 100 }
}
```

### Error
```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human readable message",
    "details": []
  }
}
```

---

## Endpoints

### Auth

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| POST | /auth/register | Register new user | ❌ |
| POST | /auth/login | Login | ❌ |
| POST | /auth/refresh | Refresh token | ❌ |
| POST | /auth/logout | Logout | ✅ |
| POST | /auth/forgot-password | Request password reset | ❌ |
| POST | /auth/reset-password | Reset password | ❌ |

#### POST /auth/register
```json
// Request
{
  "email": "user@example.com",
  "password": "securePassword123!",
  "name": "John Doe"
}

// Response 201
{
  "success": true,
  "data": {
    "user": { "id": "uuid", "email": "...", "name": "..." },
    "accessToken": "jwt...",
    "refreshToken": "jwt..."
  }
}

// Error 400
{
  "success": false,
  "error": { "code": "VALIDATION_ERROR", "message": "Email đã tồn tại" }
}
```

### Users

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| GET | /users/me | Get current user profile | ✅ |
| PATCH | /users/me | Update current user | ✅ |
| GET | /users/:id | Get user by ID (admin) | ✅ Admin |
| GET | /users | List users (admin) | ✅ Admin |

### [Resource Name]

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| GET | /resources | List resources | ✅ |
| POST | /resources | Create resource | ✅ |
| GET | /resources/:id | Get resource | ✅ |
| PATCH | /resources/:id | Update resource | ✅ |
| DELETE | /resources/:id | Delete resource | ✅ |

---

## Error Codes

| Code | HTTP Status | Description |
|---|---|---|
| VALIDATION_ERROR | 400 | Input validation failed |
| UNAUTHORIZED | 401 | Missing or invalid token |
| FORBIDDEN | 403 | Insufficient permissions |
| NOT_FOUND | 404 | Resource not found |
| CONFLICT | 409 | Duplicate resource |
| RATE_LIMITED | 429 | Too many requests |
| INTERNAL_ERROR | 500 | Server error |

## Rate Limits

| Endpoint | Limit |
|---|---|
| /auth/* | 5 req/min per IP |
| /api/* (authenticated) | 100 req/min per user |
| /api/* (public) | 30 req/min per IP |
