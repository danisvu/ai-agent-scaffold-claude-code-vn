# 🛠️ Rule: Tech Stack

> Khai báo và quản lý tech stack được phê duyệt cho dự án.

## ⚠️ QUAN TRỌNG

> Sửa file này cho phù hợp với dự án cụ thể.
> Đây là template — chọn stack phù hợp và xóa phần không dùng.

## Approved Stack

### Core Runtime
- [ ] Node.js (LTS) — JavaScript/TypeScript
- [ ] Python 3.11+ — Django/FastAPI/Flask
- [ ] Go 1.21+ — net/http, Gin, Fiber
- [ ] Rust — Actix-web, Axum

### Frontend Framework
- [ ] Next.js 14+ (React, App Router)
- [ ] Nuxt 3 (Vue 3)
- [ ] SvelteKit
- [ ] Astro (static/hybrid)

### Backend Framework
- [ ] Express.js / Fastify
- [ ] NestJS (enterprise Node.js)
- [ ] Django / Django REST Framework
- [ ] FastAPI (Python async)

### Database
- [ ] PostgreSQL (primary relational)
- [ ] MySQL / MariaDB
- [ ] MongoDB (document store)
- [ ] SQLite (dev/embedded)

### ORM / Query Builder
- [ ] Prisma (Node.js)
- [ ] Drizzle ORM (Node.js)
- [ ] SQLAlchemy (Python)
- [ ] GORM (Go)

### Caching
- [ ] Redis (cache + session + pub/sub)
- [ ] Memcached

### Queue / Background Jobs
- [ ] BullMQ (Node.js + Redis)
- [ ] Celery (Python + Redis/RabbitMQ)
- [ ] RabbitMQ

### Authentication
- [ ] NextAuth.js / Auth.js
- [ ] Passport.js
- [ ] JWT (custom implementation)
- [ ] OAuth 2.0 providers

### Testing
- [ ] Vitest / Jest (unit + integration)
- [ ] Playwright / Cypress (E2E)
- [ ] pytest (Python)

### Deployment
- [ ] Vercel
- [ ] Railway / Render
- [ ] Docker + Docker Compose
- [ ] AWS (ECS/Lambda/S3)

## Rules

1. **Không thêm dependency mới** mà không có approval
2. **Prefer built-in** trước khi thêm library
3. **Kiểm tra bundle size** trước khi thêm frontend dependency
4. **Security audit** — `npm audit` / `pip audit` định kỳ
5. **Lock file** phải commit (package-lock.json / yarn.lock / pnpm-lock.yaml)
6. **Version pinning** — dùng exact versions trong production
