---
name: security-review
description: Audit bảo mật toàn diện — authentication, input validation, secrets, dependencies.
argument-hint: "[full|quick]"
disable-model-invocation: true
---

# Security Audit Checklist

## 1. 🔐 Authentication & Authorization

- [ ] Passwords hashed bằng bcrypt (cost ≥ 12) hoặc Argon2
- [ ] JWT: access token 15m, refresh token 7d, rotation
- [ ] Cookies: Secure, HttpOnly, SameSite=Strict
- [ ] Session regenerate sau login
- [ ] Authorization checks ở mọi endpoint
- [ ] Account lockout sau N lần login fail

## 2. 🛡️ Input Validation

- [ ] Mọi user input validated server-side
- [ ] SQL injection protection (parameterized queries)
- [ ] XSS prevention (output encoding, CSP header)
- [ ] CSRF protection (SameSite cookies / tokens)
- [ ] File upload validation (type, size, content)
- [ ] Rate limiting trên auth endpoints

## 3. 🔑 Secrets & Configuration

- [ ] Không secrets trong source code
- [ ] .env files trong .gitignore
- [ ] API keys rotated định kỳ (90 ngày)
- [ ] Debug mode OFF trong production
- [ ] Error messages không leak internal info

## 4. 📡 Security Headers

- [ ] Content-Security-Policy
- [ ] X-Content-Type-Options: nosniff
- [ ] X-Frame-Options: DENY
- [ ] Strict-Transport-Security
- [ ] Referrer-Policy: strict-origin-when-cross-origin

## 5. 📦 Dependencies

- [ ] `npm audit` — no critical vulnerabilities
- [ ] Dependencies up-to-date (security patches)
- [ ] Lock file committed

## 6. 🗄️ Data Protection

- [ ] Sensitive data encrypted at rest
- [ ] HTTPS everywhere (TLS 1.2+)
- [ ] Logs không chứa passwords, tokens, credit cards
- [ ] PII minimized

## Report Template

```markdown
## Security Audit — [Date]
### Summary: Critical: X | High: X | Medium: X | Low: X
### Findings
#### [FINDING-001] [Severity]
**Issue:** [Mô tả]
**Impact:** [Ảnh hưởng]
**Fix:** [Cách sửa]
**Status:** Open | Fixed
```
