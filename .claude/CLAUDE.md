# Project

- **Tên**: ai-agent-scaffold-claude-code-vn
- **Mô tả**: Universal project scaffold tối ưu cho Claude Code (Bản Tiếng Việt)
- **Stack**: <!-- ⚠️ THAY THẾ: Điền tech stack cụ thể, VD: Next.js 15, TypeScript, Prisma, PostgreSQL, Redis -->

## Codebase Map

```
<!-- ⚠️ THAY THẾ: Cập nhật cấu trúc thư mục cụ thể khi khởi tạo dự án -->
```

## Coding Conventions

- TypeScript strict mode, không dùng `any`
- Functional components, không class components
- camelCase cho biến/hàm, PascalCase cho class/component
- Error handling bằng custom AppError class
- Structured logging (JSON format)

## Essential Commands

```bash
npm run dev       # Start dev server
npm test          # Run tests  
npm run lint      # Lint check
npm run build     # Build production
```

## Constraints & Pitfalls

- KHÔNG commit secrets vào git — dùng .env (gitignored)
- KHÔNG push trực tiếp vào `main` — luôn tạo branch
- KHÔNG swallow errors — catch phải handle hoặc re-throw
- KHÔNG dùng `console.log` — dùng logger
- KHÔNG tạo migration mới mà sửa migration cũ đã chạy

## Tài liệu

- Kiến trúc: `docs/architecture.md`
- API Spec: `docs/api-spec.md`
- Setup: `docs/setup-guide.md`
