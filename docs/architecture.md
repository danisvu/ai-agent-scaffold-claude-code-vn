# 🏗️ Architecture Document

> Tài liệu kiến trúc hệ thống — cập nhật khi architecture thay đổi.

## Overview

```
[Mô tả tổng quan kiến trúc hệ thống ở đây]
```

## System Architecture Diagram

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│   Client    │────▶│   API GW /   │────▶│   App       │
│   (Web/App) │     │   Load Bal.  │     │   Server    │
└─────────────┘     └──────────────┘     └──────┬──────┘
                                                │
                    ┌───────────────────────────┤
                    │              │             │
              ┌─────▼─────┐ ┌─────▼─────┐ ┌────▼──────┐
              │ Database  │ │   Redis   │ │  Queue    │
              │ (Primary) │ │  (Cache)  │ │ (Workers) │
              └───────────┘ └───────────┘ └───────────┘
```

## Components

### [Component 1]
- **Purpose:** [Mục đích]
- **Tech:** [Technology]
- **Scaling:** [Horizontal/Vertical]
- **Dependencies:** [What it depends on]

### [Component 2]
- **Purpose:** [Mục đích]
- **Tech:** [Technology]
- **Scaling:** [Horizontal/Vertical]
- **Dependencies:** [What it depends on]

## Data Flow

```
1. Client → API Request
2. API Gateway → Authentication + Rate Limiting
3. Controller → Input Validation
4. Service → Business Logic
5. Repository → Database Query
6. Response → Client
```

## Architecture Decision Records (ADRs)

| ID | Title | Status | Date |
|---|---|---|---|
| ADR-001 | [Quyết định 1] | Accepted | YYYY-MM-DD |
| ADR-002 | [Quyết định 2] | Proposed | YYYY-MM-DD |

> Chi tiết ADR xem tại `.claude/agents/planner.md`

## Infrastructure

| Service | Provider | Purpose |
|---|---|---|
| Hosting | [Vercel/AWS/Railway] | Application hosting |
| Database | [Supabase/RDS/PlanetScale] | Primary data store |
| Cache | [Upstash/ElastiCache] | Caching layer |
| Storage | [S3/Cloudflare R2] | File storage |
| CDN | [Cloudflare/CloudFront] | Static assets |
| Monitoring | [Sentry/DataDog] | Error tracking |

## Environments

| Environment | URL | Branch | Purpose |
|---|---|---|---|
| Development | localhost:3000 | feature/* | Local dev |
| Staging | staging.app.com | develop | QA testing |
| Production | app.com | main | Live users |
