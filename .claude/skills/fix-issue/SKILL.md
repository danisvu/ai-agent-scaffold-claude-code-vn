---
name: fix-issue
description: Workflow phân tích và sửa bug có hệ thống — root cause analysis, regression test, documentation.
argument-hint: "[issue number hoặc mô tả bug]"
---

# Bug Fix Workflow

## Bước 1: Thu thập thông tin

```
1. Bug xảy ra ở đâu? (URL, page, component)
2. Các bước reproduce?
3. Expected vs Actual behavior?
4. Error message / stack trace?
5. Môi trường? (dev/staging/prod)
```

## Bước 2: Root Cause Analysis (5 Whys)

```
Bug: [Mô tả]
Why 1: [Tại sao xảy ra?]
Why 2: [Tại sao điều đó xảy ra?]
Why 3: [Tiếp tục đào sâu...]
Why 4: [...]
Why 5: [→ Root cause]
```

## Bước 3: Fix

1. **Viết failing test** — reproduce bug bằng test
2. **Fix code** — sửa root cause, KHÔNG chỉ symptom
3. **Verify test pass**
4. **Chạy full test suite** — check regression
5. **Self-review** trước khi tạo PR

## Bước 4: Document

```markdown
### Bug Fix: [Mô tả ngắn]
**Root Cause:** [Nguyên nhân gốc]
**Fix:** [Cách sửa]
**Tests Added:** [File test mới]
**Prevention:** [Cách ngăn bug tương tự]
```

## Severity

| Level | Mô tả | SLA |
|---|---|---|
| P0 | Hệ thống sập, data loss | Fix ngay |
| P1 | Feature chính broken | 4h |
| P2 | Feature phụ lỗi, có workaround | 1-2 ngày |
| P3 | UI minor, typo | Khi có thời gian |
