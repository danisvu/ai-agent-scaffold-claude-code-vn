---
globs: "**/models/**, **/migrations/**, **/repositories/**, **/prisma/**, **/schema/**, **/*.sql"
---

# 🗄️ Rule: Database

> Quy tắc thiết kế database, queries, và migrations.

## Schema Design

### Bắt buộc cho mọi table

```sql
-- Mọi table phải có:
id          UUID PRIMARY KEY DEFAULT gen_random_uuid()
created_at  TIMESTAMPTZ NOT NULL DEFAULT NOW()
updated_at  TIMESTAMPTZ NOT NULL DEFAULT NOW()

-- Soft delete (khuyến khích):
deleted_at  TIMESTAMPTZ NULL
```

### Naming
- Tables: `snake_case`, **plural** — `users`, `order_items`
- Columns: `snake_case` — `first_name`, `is_active`
- Foreign keys: `[singular_table]_id` — `user_id`, `order_id`
- Indexes: `idx_[table]_[columns]` — `idx_users_email`
- Unique: `uniq_[table]_[columns]` — `uniq_users_email`

## Query Optimization

### N+1 Problem
```
❌ BAD: Query users, then loop query orders for each user
   SELECT * FROM users;
   SELECT * FROM orders WHERE user_id = 1;  -- x N times

✅ GOOD: Eager loading / JOIN
   SELECT u.*, o.* FROM users u
   LEFT JOIN orders o ON o.user_id = u.id;
   
   // ORM: include, eager_load, prefetch_related
   prisma.user.findMany({ include: { orders: true } })
```

### Index Strategy
```
-- Index tự động: Primary key, Unique constraints
-- Cần tạo thủ công:
1. Foreign keys (luôn tạo index)
2. Columns dùng trong WHERE frequently
3. Columns dùng trong ORDER BY
4. Composite indexes cho multi-column queries

-- Thứ tự composite index quan trọng:
CREATE INDEX idx_orders_status_date ON orders(status, created_at);
-- Query WHERE status = X AND created_at > Y → ✅ dùng index
-- Query WHERE created_at > Y → ❌ không dùng index (sai thứ tự)
```

## Migrations

```
Rules:
1. Mỗi migration làm 1 việc — không gộp nhiều changes
2. Migration phải reversible (có rollback plan)
3. KHÔNG modify migration đã chạy trên production
4. Test migration trên staging trước production
5. Backup database TRƯỚC KHI chạy migration trên production
6. Tên migration descriptive: 20240101_add_role_column_to_users
```

## Transaction Rules

```
1. Dùng transaction cho operations cần atomicity
2. Giữ transaction ngắn nhất có thể
3. Không gọi external APIs trong transaction
4. Handle deadlock: retry với exponential backoff
5. Set transaction timeout
```

## Pagination

```
-- Offset (simple, chấp nhận cho < 100k records)
SELECT * FROM users ORDER BY id LIMIT 20 OFFSET 40;

-- Cursor-based (recommended cho large datasets)
SELECT * FROM users WHERE id > $cursor ORDER BY id LIMIT 20;
```
