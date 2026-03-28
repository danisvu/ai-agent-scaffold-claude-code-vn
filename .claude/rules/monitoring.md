---
globs: "**/logger/**, **/logging/**, **/monitoring/**, **/health/**, **/metrics/**"
---

# 📊 Rule: Monitoring & Logging

> Quy tắc monitoring, alerting, và logging.

## Logging

### Log Levels
| Level | Khi nào dùng | Ví dụ |
|---|---|---|
| ERROR | Lỗi cần fix ngay | Database connection failed |
| WARN | Vấn đề tiềm ẩn | Retry attempt 3/5, Deprecated API call |
| INFO | Business events | User registered, Order placed, Payment processed |
| DEBUG | Chi tiết kỹ thuật | Query executed in 45ms, Cache hit for key X |

### Structured Logging Format
```json
{
  "timestamp": "2024-01-01T12:00:00.000Z",
  "level": "error",
  "message": "Payment processing failed",
  "service": "payment-service",
  "traceId": "abc-123",
  "userId": "user-456",
  "orderId": "order-789",
  "error": {
    "code": "STRIPE_DECLINED",
    "message": "Card declined"
  },
  "duration": 1250
}
```

### Rules
```
✅ DO:
- Structured JSON logs (not plain text)
- Include correlation/trace ID
- Log business events (user actions, state changes)
- Log external API calls (request/response time, status)
- Use appropriate log levels

❌ DON'T:
- Log passwords, tokens, credit card numbers
- Log PII without masking
- Use console.log in production (use logger)
- Log inside tight loops (performance impact)
- Log entire request/response bodies (too verbose)
```

## Health Check Endpoint

```
GET /health
{
  "status": "healthy",
  "timestamp": "2024-01-01T12:00:00Z",
  "version": "1.2.3",
  "checks": {
    "database": "ok",
    "redis": "ok",
    "queue": "ok"
  }
}
```

## Key Metrics (The Four Golden Signals)

| Signal | Metric | Alert Threshold |
|---|---|---|
| **Latency** | p95 response time | > 500ms for 5 min |
| **Traffic** | Requests per second | +/- 50% sudden change |
| **Errors** | Error rate (5xx) | > 1% for 5 min |
| **Saturation** | CPU/Memory/Disk usage | > 80% for 10 min |

## Alerting Rules

```
P0 (Page immediately):
- Service down (health check failing)
- Error rate > 5%
- Database connection pool exhausted

P1 (Page within 15 min):
- Error rate > 1%
- p95 latency > 2s
- Disk usage > 90%

P2 (Slack notification):
- Memory usage > 80%
- Queue backlog growing
- SSL certificate expiring < 30 days
```

## Tools (chọn theo stack)

- **Logging:** Pino, Winston, Python logging, Loki
- **Metrics:** Prometheus, DataDog, New Relic
- **Dashboards:** Grafana, DataDog
- **APM:** Sentry, DataDog APM, New Relic
- **Uptime:** UptimeRobot, Better Uptime
