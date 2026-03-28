---
globs: "**/config/**, **/infrastructure/**, **/docker-compose.*, **/Dockerfile, docs/architecture.*"
---

# 🏛️ Rule: System Design

> Quy tắc thiết kế hệ thống, scalability, và infrastructure.

## Architecture Patterns

### Monolith (khởi đầu)
```
app/
├── controllers/    # HTTP handlers
├── services/       # Business logic
├── repositories/   # Data access
├── middleware/      # Cross-cutting concerns
└── utils/          # Shared utilities
```
> ✅ Bắt đầu với monolith. Migrate sang microservices KHI CẦN.

### Modular Monolith (scale tiếp)
```
modules/
├── users/          # User module (self-contained)
│   ├── controller
│   ├── service
│   └── repository
├── orders/         # Order module
└── payments/       # Payment module
```

### Microservices (khi thực sự cần)
> Chỉ tách khi: team > 10 người, deploy frequency khác nhau, scale requirements khác nhau.

## Design Principles

### CAP Theorem
- **Consistency + Availability** → Single node DB (PostgreSQL)
- **Availability + Partition Tolerance** → Eventually consistent (Cassandra, DynamoDB)
- **Consistency + Partition Tolerance** → Sacrifice availability during partition (HBase)

### Caching Strategy
```
1. Cache-Aside (Lazy Loading)  — phổ biến nhất
   Read: Check cache → miss → read DB → write cache → return
   
2. Write-Through
   Write: Write cache + DB đồng thời
   
3. Write-Behind (Write-Back)
   Write: Write cache → async write DB
   
TTL Guidelines:
- Static data (countries, categories): 24h
- User profile: 1h
- Session: 30 min
- Real-time data: No cache hoặc 30s
```

### Queue Patterns
```
1. Fire-and-Forget  → Email notifications
2. Request-Reply    → Async API calls
3. Pub/Sub          → Event broadcasting
4. Dead Letter Queue → Failed message handling
```

## Scalability Checklist

- [ ] Stateless services (no server-side session storage)
- [ ] Database connection pooling
- [ ] Horizontal scaling ready (load balancer compatible)
- [ ] Async operations cho heavy tasks (queues)
- [ ] CDN cho static assets
- [ ] Database read replicas cho read-heavy workloads
- [ ] Rate limiting ở API gateway
- [ ] Circuit breaker cho external service calls

## Performance Targets

| Metric | Target |
|---|---|
| API response (p50) | < 100ms |
| API response (p95) | < 500ms |
| API response (p99) | < 1s |
| Page load (LCP) | < 2.5s |
| Time to Interactive | < 3.5s |
| Error rate | < 0.1% |
| Uptime | 99.9% |
