# 🧹 Rule: Clean Code

> Quy tắc viết code sạch, dễ đọc, dễ bảo trì.

## Nguyên tắc SOLID

### S — Single Responsibility
- Mỗi function làm **1 việc duy nhất**
- Mỗi class/module có **1 lý do duy nhất để thay đổi**
- Nếu bạn cần dùng "and" để mô tả function → tách ra

### O — Open/Closed
- Open for extension, Closed for modification
- Dùng interfaces, abstract classes, strategy pattern

### L — Liskov Substitution
- Subclass phải thay thế được parent class mà không break

### I — Interface Segregation
- Nhiều interface nhỏ tốt hơn 1 interface lớn
- Client không nên bị ép implement methods không dùng

### D — Dependency Inversion
- Depend on abstractions, not concretions
- Inject dependencies thông qua constructor

## Quy tắc về Functions

```
✅ DO:
- Tên function = verb + noun: getUserById(), calculateTotal()
- Tối đa 3 parameters — dùng object nếu nhiều hơn
- Một function ≤ 30 lines (khuyến khích ≤ 15)
- Return early — tránh deep nesting
- Pure functions khi có thể

❌ DON'T:
- Function quá 50 lines
- Boolean flag parameters: process(data, true)  → tách thành 2 functions
- Side effects ẩn — function name không hint về side effect
- Nesting > 3 levels
```

## Quy tắc về Variables

```
✅ DO:
- Tên biến = noun: userCount, orderTotal, isActive
- Dùng const mặc định, let khi cần reassign
- Destructuring khi truy cập object properties
- Meaningful names: remainingAttempts thay vì ra

❌ DON'T:
- Single-letter variables (trừ loop index i, j)
- Abbreviations khó hiểu: usrCnt, ordTtl
- var (dùng const/let)
- Magic numbers: if (status === 3) → if (status === STATUS.ACTIVE)
```

## Quy tắc về Comments

```
✅ DO:
- Comment WHY, không phải WHAT
- JSDoc/docstring cho public APIs
- TODO format: // TODO(author): description — YYYY-MM-DD

❌ DON'T:
- // increment i by 1  (obvious comment)
- Commented-out code — xóa đi, git đã lưu
- Journal comments — dùng git log
```
