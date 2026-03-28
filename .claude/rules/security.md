# 🔒 Rule: Security

> ⚠️ CRITICAL — Quy tắc bảo mật bắt buộc.

## Authentication

```
1. Passwords PHẢI hash bằng bcrypt (cost ≥ 12) hoặc Argon2
2. JWT tokens:
   - Access token: short-lived (15 min)
   - Refresh token: long-lived (7 days), stored httpOnly cookie
   - Rotate refresh token mỗi lần sử dụng
3. Session:
   - Secure, HttpOnly, SameSite=Strict cookies
   - Regenerate session ID sau login
4. MFA khuyến khích cho admin accounts
```

## Input Validation

```
1. VALIDATE MỌI INPUT từ client — KHÔNG TIN BẤT CỨ GÌ
2. Whitelist approach: chỉ accept known-good input
3. Validate type, length, range, format
4. Sanitize HTML input (DOMPurify / bleach)
5. Parameterized queries — KHÔNG BAO GIỜ string concatenation cho SQL
```

## Common Vulnerabilities

### SQL Injection
```
❌ `SELECT * FROM users WHERE id = '${userId}'`
✅ `SELECT * FROM users WHERE id = $1` + [userId]
✅ ORM queries (Prisma, SQLAlchemy)
```

### XSS (Cross-Site Scripting)
```
❌ innerHTML = userInput
✅ textContent = userInput
✅ Framework auto-escaping (React JSX, Vue templates)
✅ Content-Security-Policy header
```

### CSRF
```
✅ SameSite=Strict cookies
✅ CSRF tokens cho forms
✅ Verify Origin/Referer headers
```

## Security Headers

```
Content-Security-Policy: default-src 'self'
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
X-XSS-Protection: 0
Strict-Transport-Security: max-age=31536000; includeSubDomains
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: camera=(), microphone=(), geolocation=()
```

## Secrets Management

```
1. KHÔNG BAO GIỜ commit secrets vào git
2. Dùng .env files (gitignored) cho local
3. Dùng platform secrets (Vercel, Railway) cho production
4. Rotate secrets định kỳ (90 ngày)
5. Tách secrets theo environment (dev/staging/prod)
```

## Data Protection

```
1. Encrypt sensitive data at rest (AES-256)
2. HTTPS everywhere (TLS 1.2+)
3. PII: minimize collection, encrypt storage
4. Logs: KHÔNG log passwords, tokens, credit cards
5. GDPR/Data privacy: right to deletion
```

## Rate Limiting

```
- Public APIs: 100 req/min per IP
- Auth endpoints: 5 req/min per IP (brute-force prevention)
- Authenticated APIs: 1000 req/min per user
- File upload: 10 req/min per user
```
