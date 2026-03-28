# 📛 Rule: Naming Conventions

> Quy tắc đặt tên thống nhất cho mọi thực thể trong dự án.

## Biến môi trường

```bash
# Format: UPPER_SNAKE_CASE
# Prefix theo nhóm
APP_NAME=my-app
APP_ENV=production
APP_PORT=3000

DATABASE_URL=postgresql://...
DATABASE_POOL_SIZE=10

REDIS_URL=redis://...
REDIS_TTL=3600

JWT_SECRET=xxx
JWT_EXPIRES_IN=7d

SMTP_HOST=smtp.gmail.com
SMTP_PORT=587

AWS_ACCESS_KEY_ID=xxx
AWS_S3_BUCKET=my-bucket
```

## Database

```sql
-- Tables: snake_case, plural
users, order_items, product_categories

-- Columns: snake_case
first_name, created_at, is_active, total_amount

-- Primary key: id (UUID hoặc bigint auto-increment)
-- Foreign key: [table_singular]_id
user_id, order_id, category_id

-- Indexes: idx_[table]_[columns]
idx_users_email, idx_orders_user_id_created_at

-- Enums: UPPER_SNAKE_CASE
ORDER_PENDING, ORDER_COMPLETED, ROLE_ADMIN
```

## Cache Keys

```
# Format: [domain]:[entity]:[identifier]:[attribute?]
user:123                    # user object
user:123:profile            # user profile
user:email:john@ex.com      # lookup by email
order:456:items             # order items
session:abc-def-ghi         # session data
rate-limit:ip:192.168.1.1   # rate limit counter

# TTL naming:
CACHE_TTL_SHORT=300         # 5 min
CACHE_TTL_MEDIUM=3600       # 1 hour
CACHE_TTL_LONG=86400        # 1 day
```

## Message Queues

```
# Queue names: kebab-case
email-notifications
order-processing
image-resizing
report-generation

# Job types: DOMAIN.ACTION
user.welcome-email
order.process-payment
image.generate-thumbnail
```

## API Endpoints

```
# Format: /api/v[N]/[resource-plural]
GET    /api/v1/users           # list
POST   /api/v1/users           # create
GET    /api/v1/users/:id       # get one
PATCH  /api/v1/users/:id       # update
DELETE /api/v1/users/:id       # delete

# Nested resources
GET    /api/v1/users/:id/orders
POST   /api/v1/users/:id/orders

# Actions (non-CRUD)
POST   /api/v1/users/:id/activate
POST   /api/v1/orders/:id/cancel
```

## Git Branches

```
# Format: [type]/[ticket-id]-[short-description]
feature/PM-123-add-user-auth
bugfix/PM-456-fix-login-error
hotfix/PM-789-security-patch
chore/PM-012-update-deps
refactor/PM-345-extract-service
```
