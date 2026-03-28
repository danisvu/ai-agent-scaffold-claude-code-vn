# 🚀 Setup Guide

> Hướng dẫn cài đặt và chạy dự án cho developer mới.

## Yêu cầu hệ thống

- [ ] Node.js ≥ 18 (hoặc runtime phù hợp)
- [ ] Git ≥ 2.30
- [ ] Docker & Docker Compose (optional, cho database local)
- [ ] Editor: VS Code (khuyến khích) + Extensions

### VS Code Extensions khuyến khích

- ESLint
- Prettier
- GitLens
- Error Lens
- Thunder Client (API testing)
- Database Client

## Bước 1: Clone & Install

```bash
# Clone repo
git clone <repo-url>
cd <project-name>

# Install dependencies
npm install       # Node.js
# pip install -r requirements.txt  # Python
# go mod download                  # Go
```

## Bước 2: Environment Setup

```bash
# Copy env template
cp .env.example .env

# Sửa .env với thông tin local:
# - DATABASE_URL
# - REDIS_URL
# - JWT_SECRET (generate: openssl rand -hex 32)
```

## Bước 3: Database Setup

```bash
# Option A: Docker (khuyến khích)
docker compose up -d

# Option B: Local installation
# PostgreSQL: brew install postgresql@16
# Redis: brew install redis

# Run migrations
npx prisma migrate dev    # Prisma
# python manage.py migrate  # Django
# goose up                  # Go
```

## Bước 4: Run Development Server

```bash
# Start dev server
npm run dev

# Server chạy tại:
# http://localhost:3000
```

## Bước 5: Verify Setup

```bash
# Run tests
npm test

# Health check
curl http://localhost:3000/health
```

## Cấu trúc thư mục

```
[Mô tả cấu trúc thư mục cụ thể của dự án ở đây]
```

## Scripts thường dùng

| Command | Mô tả |
|---|---|
| `npm run dev` | Start development server |
| `npm test` | Run tests |
| `npm run lint` | Run linter |
| `npm run build` | Build production |
| `npm run db:migrate` | Run database migrations |
| `npm run db:seed` | Seed database |
| `npm run db:studio` | Open database GUI |

## Troubleshooting

### Port đã bị sử dụng
```bash
lsof -ti:3000 | xargs kill -9
```

### Database connection failed
```bash
# Kiểm tra Docker container
docker ps
docker compose logs db

# Kiểm tra connection string trong .env
```

### Dependencies lỗi
```bash
rm -rf node_modules package-lock.json
npm install
```

## Tài liệu liên quan

- [Architecture](./architecture.md)
- [API Documentation](./api-spec.md)
- [Claude Code Rules](../.claude/CLAUDE.md)
