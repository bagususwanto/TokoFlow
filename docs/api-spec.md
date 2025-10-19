# Spesifikasi API

## Autentikasi

### POST /api/auth/login

- **Request:** `{ username, password }`
- **Response:** `{ token, role }`

---

## Barang

### GET /api/products

- **Response:** Daftar semua barang.

### POST /api/products

- **Body:** `{ name, category, price, stock, barcode }`

### PUT /api/products/:id

- **Body:** `{ name?, category?, price?, stock? }`

### DELETE /api/products/:id

- **Response:** `204 No Content`

---

## Transaksi

### POST /api/sales

- **Body:** `{ items: [{ product_id, quantity }], total_price }`
- **Response:** `{ sale_id, created_at }`

### GET /api/sales?from=2025-10-01&to=2025-10-18

- **Response:** Daftar transaksi per periode
