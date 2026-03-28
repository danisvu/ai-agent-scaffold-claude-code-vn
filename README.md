# 🤖 AI-Agent Scaffold for Claude Code

> Universal project scaffold tối ưu cho Claude Code.
> Clone → Configure → Code. Hoạt động với **mọi** tech stack.

## 📋 Quick Start

```bash
# 1. Clone scaffold
git clone <repo-url> my-project && cd my-project

# 2. Reset git
rm -rf .git && git init

# 3. Cấu hình CLAUDE.md (BẮT BUỘC)
# Sửa .claude/CLAUDE.md — điền tên, stack, conventions

# 4. Bắt đầu code với Claude Code!
```

## 🏗️ Cấu trúc

```
.claude/                          # 🧠 AI Agent Configuration
├── CLAUDE.md                     # Master AI Instructions (SỬA ĐẦU TIÊN)
├── CLAUDE.local.md               # Local overrides (gitignored)
├── settings.json                 # Permissions + Hooks
├── settings.local.json           # Local settings (gitignored)
│
├── agents/                       # 🎭 AI Subagents (5 agents)
│   ├── frontend.md               # UI/UX implementation, components
│   ├── backend.md                # API, database, auth, caching
│   ├── qa.md                     # Testing, coverage, bug reproduction
│   ├── planner.md                # Architecture + Project management
│   └── designer.md               # UI design + SEO + Microcopy
│
├── skills/                       # 🛠 Slash commands (/skill-name)
│   ├── deploy/SKILL.md           # /deploy — triển khai ứng dụng
│   ├── fix-issue/SKILL.md        # /fix-issue — phân tích & sửa bug
│   ├── review/SKILL.md           # /review — code review checklist
│   └── security-review/SKILL.md  # /security-review — audit bảo mật
│
└── rules/                        # 📏 Auto-loaded rules
    ├── clean-code.md              # SOLID, functions, variables
    ├── code-style.md              # Formatting, naming conventions
    ├── error-handling.md          # AppError, response format
    ├── naming-conventions.md      # Env, DB, cache, queue, API, git
    ├── tech-stack.md              # Approved technologies
    ├── system-design.md           # Architecture, caching, scaling
    ├── project-structure.md       # Folder layout by framework
    ├── api-conventions.md         # REST, pagination, versioning
    ├── database.md                # Schema, queries, migrations
    ├── security.md                # Auth, validation, headers
    ├── monitoring.md              # Logging, metrics, alerting
    ├── testing.md                 # Pyramid, coverage, patterns
    └── git-workflow.md            # Branching, conventional commits

docs/                             # 📖 Tài liệu dự án
├── architecture.md
├── api-spec.md
└── setup-guide.md

.env.example                      # 🔐 Template biến môi trường
.gitignore                        # Git ignore rules
```

## 🎯 Cách sử dụng

### Agents — Gọi chuyên gia AI
Claude tự động chọn agent phù hợp, hoặc bạn có thể gọi trực tiếp:
```
Sử dụng agent frontend để tạo component UserProfile
Sử dụng agent planner để thiết kế kiến trúc cho module payment
```

### Skills — Slash commands
```
/deploy staging          # Triển khai lên staging
/fix-issue PM-123        # Phân tích và sửa bug
/review src/services/    # Code review
/security-review full    # Audit bảo mật
```

### Rules — Tự động áp dụng
Files trong `rules/` được Claude tự động load mỗi session.
Không cần gọi — chúng luôn active.

## 🔄 Tùy chỉnh cho dự án mới

| File | Hành động |
|---|---|
| `.claude/CLAUDE.md` | **Bắt buộc sửa** — tên, stack, conventions |
| `.claude/rules/tech-stack.md` | Tick checkbox stack cụ thể |
| `.env.example` | Thêm variables cho dự án |
| `docs/architecture.md` | Mô tả kiến trúc hệ thống |

## 📜 License

MIT — Free to use, modify, and distribute.
