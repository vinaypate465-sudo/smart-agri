# Smart Agriculture Management & Farmer Marketplace

Java full-stack web app: **React.js + Spring Boot 3 (Java 17) + MySQL**, secured with **JWT + Spring Security**.

## Run it

### 1. Database
```sql
CREATE DATABASE smart_agri;
```

### 2. Backend  (http://localhost:8080)
Edit `backend/src/main/resources/application.properties` and set `spring.datasource.password`.
```
cd backend
mvn spring-boot:run
```
Tables are created automatically. On first run a default admin and starter advisory content are added:

| Role  | Email                | Password |
|-------|----------------------|----------|
| Admin | admin@smartagri.com  | admin123 |

(Change the admin password and `app.jwt.secret` before any real deployment.)

### 3. Frontend  (http://localhost:5173)
```
cd frontend
npm install
npm run dev
```

## Roles & features

**Farmer**: farms, crops & production (yield/revenue), expenses, profit/loss dashboard with charts,
advisory (irrigation, fertilizer by crop & soil, disease symptoms & treatment), list products,
manage incoming orders and delivery status.

**Customer**: browse/search marketplace, cart, checkout (COD or simulated online payment), track/cancel orders.

**Admin**: platform stats, manage users, products, orders, and advisory content.

## REST API

| Area | Endpoints |
|------|-----------|
| Auth | `POST /api/auth/register`, `POST /api/auth/login` |
| Farmer | `/api/farms`, `/api/crops`, `/api/expenses` (GET, POST, PUT /{id}, DELETE /{id}) |
| Reports | `GET /api/reports/farmer` |
| Advisory | `GET /api/advisory?type=IRRIGATION\|FERTILIZER\|DISEASE\|PRACTICE&crop=` |
| Marketplace | `GET /api/products` (public), `GET /api/products/mine`, `POST/PUT/DELETE /api/products` |
| Orders | `POST /api/orders`, `GET /api/orders/my`, `GET /api/orders/farmer`, `PUT /api/orders/{id}/cancel`, `PUT /api/orders/{id}/status` |
| Admin | `/api/admin/stats`, `/users`, `/products`, `/orders`, `/advisory` |

## Notes
- Online payment is **simulated** (marked PAID instantly). Integrate Razorpay/Stripe for real payments.
- Advisory content is rule-based starter data; verify doses with a soil test / local agriculture officer.
