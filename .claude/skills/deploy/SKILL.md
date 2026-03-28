---
name: deploy
description: Quy trình triển khai ứng dụng — pre-checks, deployment, verification, rollback.
argument-hint: "[staging|production]"
disable-model-invocation: true
---

# Deploy Pipeline

## 1. Pre-deploy Checks

```bash
git status --porcelain          # Branch clean?
npm test                        # Tests pass?
npm run lint                    # No lint errors?
npm run build                   # Build OK?
npm audit --production          # No vulnerabilities?
```

## 2. Create Release

```bash
npm version patch|minor|major
git tag -a v1.x.x -m "Release v1.x.x"
git push origin main --tags
```

## 3. Deploy

```bash
# Vercel:  vercel --prod
# Railway: railway up
# Docker:  docker build -t app . && docker push
# AWS:     aws ecs update-service ...
```

## 4. Post-deploy Verification

```bash
curl -sf https://your-app.com/health | jq .
npm run test:smoke
# Monitor error rate 5 phút đầu
```

## 5. Rollback (nếu cần)

```bash
git revert HEAD && git push origin main
# Vercel: vercel rollback
# Docker: kubectl rollout undo deployment/app
```

## Checklist

- [ ] Tests pass
- [ ] No lint errors
- [ ] Build succeeds
- [ ] DB migrations prepared
- [ ] Env vars updated on hosting
- [ ] Health check passes after deploy
- [ ] Monitoring shows no errors
- [ ] Team notified
