# API Spec - TokoFlow (with Examples)

Dokumen API Spec ini mendukung pengembangan backend (Express + Sequelize) dan integrasi frontend (React), **MVP fokus**. Ditambahkan contoh request/response.

---

## Konvensi Umum

- Base URL: `/api/v1`
- Autentikasi: **Bearer token (JWT)**
- Format request/response: `application/json`
- Pagination: `?page=1&limit=20`
- Sorting: `?sort=field` atau `?sort=-field`
- Filter: query params sesuai resource
- Error: `{ code, message, details? }`

---

## 1. Authentication

### POST /auth/login

**Request:**

```json
{
  "username": "admin",
  "password": "admin123"
}
```

**Response 200:**

```json
{
  "accessToken": "eyJhbGci...",
  "refreshToken": "eyJhbGci...",
  "user": {
    "id": "uuid-1234",
    "username": "admin",
    "role": "owner",
    "storeId": null
  }
}
```

### POST /auth/refresh

**Request:**

```json
{ "refreshToken": "eyJhbGci..." }
```

**Response 200:**

```json
{ "accessToken": "new-access-token", "refreshToken": "new-refresh-token" }
```

### POST /auth/logout

**Request:**

```json
{ "refreshToken": "eyJhbGci..." }
```

**Response 204:** No Content

---

## 2. Users

### GET /users

**Query:** `?page=1&limit=10&role=kasir`
**Response 200:**

```json
{
  "data": [
    {
      "id": "uuid-1",
      "username": "kasir1",
      "role": "kasir",
      "storeId": "store-uuid"
    }
  ],
  "meta": { "page": 1, "limit": 10, "total": 50 }
}
```

### POST /users

**Request:**

```json
{
  "username": "kasir2",
  "password": "123456",
  "fullName": "Kasir Dua",
  "role": "kasir",
  "storeId": "store-uuid",
  "isActive": true
}
```

**Response 201:**

```json
{
  "id": "uuid-2",
  "username": "kasir2",
  "role": "kasir",
  "storeId": "store-uuid",
  "isActive": true
}
```

### PUT /users/:id

**Request:**

```json
{ "fullName": "Kasir 2 Updated" }
```

**Response 200:** Updated user object

### DELETE /users/:id

**Response 204:** No Content

---

## 3. Stores

### POST /stores

**Request:**

```json
{ "name": "Toko A", "address": "Jl. Merdeka 1" }
```

**Response 201:**

```json
{ "id": "store-uuid", "name": "Toko A", "address": "Jl. Merdeka 1" }
```

---

## 4. Products

### POST /products

**Request:**

```json
{
  "sku": "PRD001",
  "name": "Produk A",
  "categoryId": null,
  "unit": "pcs",
  "costPrice": 5000,
  "salePrice": 8000,
  "barcode": "1234567890123",
  "isActive": true
}
```

**Response 201:**

```json
{
  "id": "product-uuid",
  "sku": "PRD001",
  "name": "Produk A",
  "unit": "pcs",
  "costPrice": 5000,
  "salePrice": 8000,
  "isActive": true
}
```

---

## 5. Inventory

### POST /inventory

**Request:**

```json
{
  "storeId": "store-uuid",
  "productId": "product-uuid",
  "type": "IN",
  "quantity": 100,
  "reason": "Initial stock"
}
```

**Response 201:**

```json
{
  "id": "inventory-move-uuid",
  "storeId": "store-uuid",
  "productId": "product-uuid",
  "type": "IN",
  "quantity": 100
}
```

---

## 6. POS / Sales

### POST /sales

**Request:**

```json
{
  "storeId": "store-uuid",
  "userId": "user-uuid",
  "items": [
    {
      "productId": "product-uuid",
      "sku": "PRD001",
      "name": "Produk A",
      "unitPrice": 8000,
      "quantity": 2,
      "discount": 0
    }
  ],
  "payment": { "method": "CASH", "amount": 16000, "change": 0 },
  "notes": "Transaksi contoh",
  "status": "SAVED"
}
```

**Response 201:**

```json
{
  "id": "sale-uuid",
  "receiptNo": "INV/2025/10/001",
  "total": 16000,
  "createdAt": "2025-10-21T12:00:00Z"
}
```

---

## 7. Reports

### GET /reports/daily-sales?storeId=store-uuid&date=2025-10-21

**Response 200:**

```json
{
  "storeId": "store-uuid",
  "date": "2025-10-21",
  "totalSales": 16000,
  "transactionsCount": 1
}
```

---

## 8. Audit Trail

### GET /audit?page=1&limit=10

**Response 200:**

```json
{
  "data": [
    {
      "id": "log-uuid",
      "userId": "user-uuid",
      "module": "PRODUCT",
      "action": "UPDATE",
      "before": { "salePrice": 5000 },
      "after": { "salePrice": 8000 },
      "createdAt": "2025-10-21T10:05:00Z"
    }
  ],
  "meta": { "page": 1, "limit": 10, "total": 50 }
}
```

---

Dokumen ini sudah termasuk **contoh request & response** untuk endpoint kunci. Bisa langsung dipakai sebagai referensi frontend atau testing API.
