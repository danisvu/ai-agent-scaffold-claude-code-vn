---
globs: "**/*.test.*, **/*.spec.*, **/tests/**, **/test/**, **/__tests__/**"
---

# 🧪 Rule: Testing

> Quy tắc viết test và coverage standards.

## Testing Pyramid

```
          /    E2E    \        5-10% — Critical user flows
         /  Integration \      20-30% — API, DB integration
        /     Unit       \     60-70% — Business logic, utils
```

## Coverage Targets

| Layer | Minimum Coverage |
|---|---|
| Business logic (services) | 80% |
| Utilities / helpers | 90% |
| Controllers / routes | 70% |
| Overall project | 75% |

## Naming Convention

```
describe('[Module/Class]', () => {
  describe('[method/function]', () => {
    it('should [expected behavior] when [condition]', () => {
      // Arrange → Act → Assert
    });
  });
});

// Ví dụ:
describe('UserService', () => {
  describe('createUser', () => {
    it('should create user successfully when valid data provided', ...);
    it('should throw VALIDATION_ERROR when email is invalid', ...);
    it('should throw CONFLICT when email already exists', ...);
  });
});
```

## Test Structure (AAA Pattern)

```typescript
it('should calculate total with discount', () => {
  // Arrange — setup test data
  const items = [{ price: 100, qty: 2 }, { price: 50, qty: 1 }];
  const discount = 0.1; // 10%

  // Act — execute the code being tested
  const total = calculateTotal(items, discount);

  // Assert — verify the result
  expect(total).toBe(225); // (200 + 50) * 0.9
});
```

## Rules

```
✅ DO:
- Test behavior, KHÔNG test implementation
- Mỗi test independent — không phụ thuộc thứ tự
- Test data tự tạo, tự cleanup
- One assertion per test (hoặc related assertions)
- Descriptive names — đọc tên hiểu test gì
- Test edge cases: null, empty, boundary values
- Bug fix = regression test trước, fix sau

❌ DON'T:
- Test private methods trực tiếp
- Mock everything — chỉ mock external dependencies
- Share state giữa tests (global variables)
- Flaky tests — fix hoặc quarantine ngay
- Test framework/library internals
- Skip tests mà không có lý do documented
```

## Test Types

### Unit Test
```
- Mock: external dependencies (DB, APIs, file system)
- No mock: business logic, pure functions
- Speed: < 50ms per test
```

### Integration Test
```
- Real: database (test DB), internal services
- Mock: external APIs (stripe, email)
- Speed: < 500ms per test
- Setup: test database with migrations
```

### E2E Test
```
- Real: entire application stack
- Mock: nothing (hoặc chỉ external payment)
- Speed: < 10s per test
- Focus: critical user journeys only
```

## Test File Location

```
# Option 1: Co-located (recommended)
src/
├── services/
│   ├── user.service.ts
│   └── user.service.test.ts

# Option 2: Separate directory
src/services/user.service.ts
tests/unit/services/user.service.test.ts
```
