# 🎨 Rule: Code Style

> Quy tắc format và style thống nhất cho toàn dự án.

## General Formatting

- **Indentation:** 2 spaces (JavaScript/TypeScript) | 4 spaces (Python)
- **Line length:** Tối đa 100 chars (khuyến khích 80)
- **Trailing commas:** Luôn dùng trong multiline
- **Semicolons:** Theo convention của project (consistent)
- **Quotes:** Single quotes cho JS/TS, double quotes cho JSON

## Naming Conventions

| Type | Convention | Ví dụ |
|---|---|---|
| Variables | camelCase | `userName`, `orderTotal` |
| Functions | camelCase | `getUserById()`, `calculateTax()` |
| Classes | PascalCase | `UserService`, `OrderController` |
| Constants | UPPER_SNAKE_CASE | `MAX_RETRY_COUNT`, `API_BASE_URL` |
| Files (components) | PascalCase | `UserProfile.tsx`, `OrderCard.vue` |
| Files (utils) | kebab-case | `date-utils.ts`, `api-client.ts` |
| Database tables | snake_case (plural) | `users`, `order_items` |
| API endpoints | kebab-case | `/api/user-profiles`, `/api/order-items` |
| Env variables | UPPER_SNAKE_CASE | `DATABASE_URL`, `JWT_SECRET` |
| CSS classes | kebab-case / BEM | `card-header`, `btn--primary` |

## File Organization

```
// Thứ tự imports
1. External libraries (node_modules)
2. Internal modules (@/...)
3. Relative imports (./...)
4. Types/interfaces
5. Styles/assets

// Thứ tự trong file
1. Types / Interfaces
2. Constants
3. Helper functions (private)
4. Main export (class / function / component)
```

## Formatting Tools

- **JavaScript/TypeScript:** Prettier + ESLint
- **Python:** Black + Ruff/Flake8
- **Go:** gofmt (built-in)
- **Rust:** rustfmt (built-in)

> 💡 Cấu hình Prettier/ESLint trong project root, không dùng config mặc định.
