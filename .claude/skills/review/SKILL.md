---
name: review
description: Code review checklist toàn diện — architecture, code quality, security, performance, testing.
argument-hint: "[file path hoặc PR number]"
---

# Code Review Checklist

## 1. 🏗️ Architecture & Design

- [ ] Đúng layer (controller/service/repository)?
- [ ] Single Responsibility — mỗi function/class làm 1 việc?
- [ ] Không duplicate code (DRY)?
- [ ] Có over-engineering không?

## 2. 📝 Code Quality

- [ ] Tên biến/hàm descriptive, theo convention?
- [ ] Functions ngắn (< 30 lines)?
- [ ] Nesting depth ≤ 3?
- [ ] Comments cho WHY, không phải WHAT?
- [ ] Không magic numbers — dùng constants?
- [ ] Không console.log / debug code còn sót?

## 3. 🔒 Security

- [ ] Input validation cho user input?
- [ ] SQL injection protection?
- [ ] XSS protection?
- [ ] Auth/authz checks đúng chỗ?
- [ ] Sensitive data không log ra?

## 4. ⚡ Performance

- [ ] Database queries tối ưu (no N+1)?
- [ ] Memoization/caching khi cần?
- [ ] Không memory leak?
- [ ] Pagination cho list queries?

## 5. 🧪 Testing

- [ ] Unit tests cho business logic mới?
- [ ] Edge cases được test?
- [ ] Test coverage không giảm?

## 6. 📚 Documentation

- [ ] README/API docs cập nhật?
- [ ] JSDoc cho public functions?

## Review Response Format

```markdown
## Code Review: [File/PR]
### ✅ Approved | ❌ Changes Requested

### Findings
1. 🔴 [Critical] — [File:Line] — [Issue]
2. 🟡 [Suggestion] — [File:Line] — [Recommendation]
3. 🟢 [Nitpick] — [File:Line] — [Minor]
```
