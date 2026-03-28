---
globs: "**/package.json, **/tsconfig.json, **/pyproject.toml, **/go.mod, **/Cargo.toml"
---

# 📂 Rule: Project Structure

> Quy tắc tổ chức thư mục và file cho dự án.

## Nguyên tắc

1. **Flat > Nested** — tránh nesting quá 4 levels
2. **Colocation** — file liên quan nằm cạnh nhau
3. **Predictable** — dev mới phải đoán được file nào ở đâu
4. **Scalable** — structure phải work khi project lớn lên

## Structure By Tech Stack

### Next.js (App Router)
```
src/
├── app/                    # Routes (App Router)
│   ├── (auth)/             # Route group
│   │   ├── login/page.tsx
│   │   └── register/page.tsx
│   ├── dashboard/page.tsx
│   ├── layout.tsx
│   └── page.tsx
├── components/
│   ├── ui/                 # Reusable UI (Button, Input, Card)
│   └── features/           # Feature-specific components
├── lib/                    # Singletons (db, redis, logger)
├── services/               # Business logic
├── types/                  # TypeScript types
└── utils/                  # Pure utility functions
```

### Express / Node.js API
```
src/
├── controllers/            # HTTP request handlers
├── services/               # Business logic
├── repositories/           # Database queries
├── middleware/              # Auth, logging, error handler
├── routes/                 # Route definitions
├── models/                 # Data models / schemas
├── config/                 # App configuration
├── utils/                  # Helper functions
├── types/                  # TypeScript types
└── index.ts                # Entry point
```

### Python / Django
```
project/
├── apps/
│   ├── users/              # User app
│   ├── orders/             # Order app
│   └── payments/           # Payment app
├── config/                 # Settings, URLs, WSGI
├── templates/              # HTML templates
├── static/                 # Static assets
└── manage.py
```

## File Naming Rules

| Type | Convention | Ví dụ |
|---|---|---|
| Component | PascalCase | `UserProfile.tsx` |
| Utility | kebab-case | `date-utils.ts` |
| Test | *.test.* hoặc *.spec.* | `user.service.test.ts` |
| Type/Interface | PascalCase | `User.types.ts` |
| Config | kebab-case | `database.config.ts` |
| Middleware | kebab-case | `auth.middleware.ts` |
| Migration | timestamp prefix | `20240101_create_users.sql` |

## Quan trọng

- **Không tạo thư mục trống** — tạo khi có file đầu tiên
- **Index files** — dùng `index.ts` cho barrel exports, nhưng KHÔNG lạm dụng
- **Tách concerns** — UI / Logic / Data access giữ riêng biệt
- **Shared code** → `lib/` hoặc `utils/`, KHÔNG duplicate
