---
globs: "**/.github/**, **/.gitlab-ci.*, **/Jenkinsfile, **/.husky/**"
---

# 🔀 Rule: Git Workflow

> Quy tắc Git Flow, branching, và commit conventions.

## Branch Strategy

```
main            ← Production code (protected)
├── develop     ← Integration branch
├── feature/*   ← New features
├── bugfix/*    ← Bug fixes
├── hotfix/*    ← Production emergency fixes
├── release/*   ← Release preparation
└── chore/*     ← Maintenance tasks
```

## Branch Naming

```
Format: [type]/[ticket-id]-[short-description]

feature/PM-123-add-user-auth
bugfix/PM-456-fix-login-error
hotfix/PM-789-security-patch
chore/PM-012-update-deps
refactor/PM-345-extract-service
docs/PM-678-update-api-docs
```

## Conventional Commits

```
Format: <type>(<scope>): <description>

Types:
  feat:     New feature
  fix:      Bug fix
  docs:     Documentation only
  style:    Formatting (no code change)
  refactor: Code restructuring (no behavior change)
  perf:     Performance improvement
  test:     Adding/updating tests
  chore:    Build, CI, dependencies
  ci:       CI/CD configuration
  revert:   Revert previous commit

Examples:
  feat(auth): add JWT refresh token rotation
  fix(api): handle null response from payment gateway
  docs(readme): update deployment instructions
  refactor(user): extract validation to separate module
  perf(db): add composite index on orders table
  test(cart): add edge case tests for empty cart
  chore(deps): upgrade prisma to v5.10
```

## Commit Rules

```
1. Mỗi commit = 1 logical change (atomic)
2. Commit message bằng tiếng Anh
3. Present tense: "add feature" KHÔNG "added feature"
4. Lowercase first word after type
5. Không ending period trong subject line
6. Body (optional): explain WHY, not WHAT
7. Max 72 chars cho subject line
```

## Pull Request

```markdown
## PR Template

### Description
[What does this PR do?]

### Type of change
- [ ] Feature
- [ ] Bug fix
- [ ] Refactor
- [ ] Documentation

### Checklist
- [ ] Code follows project conventions
- [ ] Tests added/updated
- [ ] Documentation updated
- [ ] No console.log / debug code
- [ ] Self-reviewed

### Testing
[How was this tested?]

### Screenshots (if UI change)
[Before/After screenshots]
```

## Merge Strategy

```
1. feature → develop: Squash merge
2. develop → main: Merge commit
3. hotfix → main: Merge commit + cherry-pick to develop
```

## Rules

1. **Không push trực tiếp** vào `main` hoặc `develop`
2. **Rebase before merge** — giữ history sạch
3. **Squash commits** khi merge feature branch
4. **Delete branch** sau khi merge
5. **Tag releases** — `v1.0.0`, `v1.1.0`
6. **Semver** — MAJOR.MINOR.PATCH
