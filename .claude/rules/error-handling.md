# 🚨 Rule: Error Handling

> Quy tắc xử lý lỗi thống nhất trong toàn dự án.

## Nguyên tắc cốt lõi

1. **Không bao giờ swallow errors** — catch phải handle hoặc re-throw
2. **Fail fast** — validate input sớm nhất có thể
3. **User-facing errors** phải rõ ràng và actionable
4. **Dev-facing errors** phải có đủ context để debug

## Custom Error Class

```typescript
// Ví dụ với TypeScript/JavaScript
class AppError extends Error {
  constructor(
    public statusCode: number,
    public code: string,
    message: string,
    public isOperational: boolean = true
  ) {
    super(message);
    this.name = 'AppError';
  }
}

// Sử dụng
throw new AppError(404, 'USER_NOT_FOUND', 'User không tồn tại');
throw new AppError(400, 'VALIDATION_ERROR', 'Email không hợp lệ');
throw new AppError(403, 'FORBIDDEN', 'Bạn không có quyền truy cập');
```

## Error Response Format

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Email không hợp lệ",
    "details": [
      { "field": "email", "message": "Phải là email hợp lệ" }
    ]
  }
}
```

## Error Handling by Layer

```
Controller:  Catch errors → format response → send to client
Service:     Throw AppError với business context
Repository:  Throw AppError khi database fails
Middleware:  Global error handler → log + format + respond
```

## Rules

```
✅ DO:
- Dùng custom AppError class
- Log error đầy đủ (message, stack, context)
- Phân biệt Operational vs Programming errors
- Return human-readable error messages cho client
- Validate input ở boundary (controller/API layer)

❌ DON'T:
- catch (err) {} — empty catch
- throw new Error('error') — không có error code
- Log sensitive data (passwords, tokens) trong error
- Expose stack trace cho production client
- Use try/catch cho flow control
```

## HTTP Status Codes

| Code | Khi nào dùng |
|---|---|
| 400 | Bad Request — input validation failed |
| 401 | Unauthorized — chưa đăng nhập |
| 403 | Forbidden — không có quyền |
| 404 | Not Found — resource không tồn tại |
| 409 | Conflict — duplicate, race condition |
| 422 | Unprocessable — logic validation failed |
| 429 | Too Many Requests — rate limited |
| 500 | Internal Server Error — lỗi không mong đợi |
