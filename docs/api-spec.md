# API Spec – TokoFlow

Dokumen ini menjelaskan spesifikasi API backend TokoFlow untuk versi SaaS berbasis cloud. API ini digunakan oleh frontend (React + Material UI) dan mendukung multi-tenant architecture, JWT authentication, serta subscription-based access control.

---

## 🧩 Konvensi Umum

| Keterangan   | Nilai                             |
| ------------ | --------------------------------- |
| Base URL     | `/api/v1`                         |
| Autentikasi  | `Bearer <JWT_ACCESS_TOKEN>`       |
| Format       | `application/json`                |
| Pagination   | `?page=1&limit=20`                |
| Sorting      | `?sort=field` atau `?sort=-field` |
| Filter       | Query params per resource         |
| Error Format | `{ code, message, details? }`     |

---

## 🔐 1. Authentication & User Session

### POST /auth/register

Membuat akun baru (owner) untuk SaaS TokoFlow.

```json
Request
{
  "fullName": "Budi Santoso",
  "email": "budi@example.com",
  "password": "123456",
  "storeName": "Toko Budi"
}
```

```json
Response 201
{
  "message": "Account created successfully",
  "user": {
    "id": "uuid-owner",
    "fullName": "Budi Santoso",
    "email": "budi@example.com",
    "role": "owner"
  },
  "store": {
    "id": "store-uuid",
    "name": "Toko Budi"
  },
  "subscription": {
    "plan": "Free",
    "expiresAt": "2025-11-21"
  }
}
```

### POST /auth/login

```json
Request
{ "email": "budi@example.com", "password": "123456" }
```

```json
Response 200
{
  "accessToken": "eyJhbGci...",
  "refreshToken": "eyJhbGci...",
  "user": {
    "id": "uuid-1234",
    "fullName": "Budi Santoso",
    "role": "owner",
    "storeId": "store-uuid"
  }
}
```

### POST /auth/refresh

```json
Request
{ "refreshToken": "eyJhbGci..." }
```

```json
Response 200
{
  "accessToken": "new-access-token",
  "refreshToken": "new-refresh-token"
}
```

### POST /auth/logout

```json
Request
{ "refreshToken": "eyJhbGci..." }
```

Response: **204 No Content**

---

## 👥 2. User Management

### GET /users

Query: `?page=1&limit=10&role=kasir`

```json
Response 200
{
  "data": [
    {
      "id": "uuid-1",
      "fullName": "Kasir 1",
      "email": "kasir1@tokobudi.id",
      "role": "kasir",
      "storeId": "store-uuid"
    }
  ],
  "meta": { "page": 1, "limit": 10, "total": 5 }
}
```

### POST /users

```json
Request
{
  "fullName": "Kasir Dua",
  "email": "kasir2@tokobudi.id",
  "password": "123456",
  "role": "kasir",
  "storeId": "store-uuid"
}
```

```json
Response 201
{
  "id": "uuid-2",
  "fullName": "Kasir Dua",
  "role": "kasir",
  "storeId": "store-uuid",
  "isActive": true
}
```

### PUT /users/:id

```json
Request
{ "fullName": "Kasir Dua (Updated)" }
```

Response **200**: Updated user object

### DELETE /users/:id

Menghapus user dari tenant aktif.
Response **204 No Content**

---

## 🏬 3. Store Management

### POST /stores

```json
Request
{
  "name": "Toko Cabang 2",
  "address": "Jl. Merdeka 21",
  "phone": "081234567890"
}
```

```json
Response 201
{
  "id": "store-uuid-2",
  "name": "Toko Cabang 2",
  "address": "Jl. Merdeka 21",
  "ownerId": "uuid-owner"
}
```

### GET /stores

```json
Response 200
{
  "data": [
    { "id": "store-uuid", "name": "Toko Utama" },
    { "id": "store-uuid-2", "name": "Toko Cabang 2" }
  ]
}
```

---

## 📦 4. Product Management

### POST /products

```json
Request
{
  "sku": "PRD001",
  "name": "Minyak Goreng",
  "unit": "liter",
  "costPrice": 15000,
  "salePrice": 20000,
  "storeId": "store-uuid",
  "categoryId": null
}
```

```json
Response 201
{
  "id": "product-uuid",
  "name": "Minyak Goreng",
  "sku": "PRD001",
  "unit": "liter",
  "salePrice": 20000
}
```

### GET /products?storeId=store-uuid

```json
Response 200
{
  "data": [
    { "id": "product-uuid", "name": "Minyak Goreng", "stock": 20 },
    { "id": "product-uuid2", "name": "Sabun", "stock": 15 }
  ]
}
```

---

## 📊 5. Inventory (Stock Movement)

### POST /inventory

```json
Request
{
  "storeId": "store-uuid",
  "productId": "product-uuid",
  "type": "IN",
  "quantity": 100,
  "reason": "Initial Stock"
}
```

```json
Response 201
{
  "id": "inventory-uuid",
  "storeId": "store-uuid",
  "productId": "product-uuid",
  "type": "IN",
  "quantity": 100,
  "createdAt": "2025-10-21T12:00:00Z"
}
```

GET /inventory?storeId=store-uuid → menampilkan semua pergerakan stok.

---

## 💰 6. POS / Sales

### POST /sales

```json
Request
{
  "storeId": "store-uuid",
  "userId": "user-uuid",
  "items": [
    {
      "productId": "product-uuid",
      "sku": "PRD001",
      "name": "Minyak Goreng",
      "unitPrice": 20000,
      "quantity": 2
    }
  ],
  "payment": { "method": "CASH", "amount": 40000, "change": 0 },
  "notes": "Penjualan harian",
  "status": "SAVED"
}
```

```json
Response 201
{
  "id": "sale-uuid",
  "receiptNo": "INV/2025/10/001",
  "total": 40000,
  "createdAt": "2025-10-21T12:30:00Z"
}
```

---

## 📈 7. Reports

### GET /reports/daily-sales?storeId=store-uuid&date=2025-10-21

```json
Response 200
{
  "storeId": "store-uuid",
  "date": "2025-10-21",
  "totalSales": 400000,
  "transactionsCount": 25
}
```

### GET /reports/monthly-summary?month=10&year=2025

```json
Response 200
{
  "month": "October",
  "year": 2025,
  "totalSales": 12000000,
  "topProducts": [
    { "name": "Minyak Goreng", "qty": 120 },
    { "name": "Sabun", "qty": 80 }
  ]
}
```

---

## 📜 8. Audit Trail

### GET /audit?page=1&limit=10

```json
Response 200
{
  "data": [
    {
      "id": "log-uuid",
      "userId": "user-uuid",
      "module": "PRODUCT",
      "action": "UPDATE",
      "before": { "salePrice": 18000 },
      "after": { "salePrice": 20000 },
      "createdAt": "2025-10-21T10:05:00Z"
    }
  ],
  "meta": { "page": 1, "limit": 10, "total": 50 }
}
```

---

## 💳 9. Subscription & Billing (SaaS Specific)

### GET /subscriptions/plans

Menampilkan daftar paket langganan.

```json
Response 200
{
  "data": [
    { "id": "plan-free", "name": "Free", "price": 0, "storeLimit": 1 },
    { "id": "plan-basic", "name": "Basic", "price": 49000, "storeLimit": 3 },
    { "id": "plan-pro", "name": "Pro", "price": 99000, "storeLimit": 10 }
  ]
}
```

### POST /subscriptions/checkout

```json
Request
{
  "planId": "plan-pro",
  "paymentMethod": "midtrans"
}
```

```json
Response 201
{
  "paymentUrl": "https://app.midtrans.com/pay/txn123",
  "status": "PENDING"
}
```

---

## 🧠 10. Error Responses (Umum)

| Code | Message               | Keterangan                 |
| ---- | --------------------- | -------------------------- |
| 401  | Unauthorized          | Token invalid atau expired |
| 403  | Forbidden             | Role tidak diizinkan       |
| 404  | Not Found             | Data tidak ditemukan       |
| 422  | Validation Error      | Input tidak valid          |
| 500  | Internal Server Error | Kesalahan server           |

---

Dokumen ini menjadi acuan utama untuk:

- Implementasi backend Express & PostgreSQL
- Integrasi frontend React (Axios service)
- Pengembangan sistem SaaS TokoFlow dengan model freemium → subscription
