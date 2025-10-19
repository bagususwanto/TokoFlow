# Spesifikasi API - Sistem Kasir & Stok Multi-Toko

## 1. Autentikasi

### POST /api/auth/login

- **Request:**

```json
{
  "username": "string",
  "password": "string"
}
```

- **Response:**

```json
{
  "access_token": "jwt_token",
  "refresh_token": "jwt_refresh_token",
  "user": {
    "id": "uuid",
    "username": "string",
    "role": "Owner/Admin/Kasir",
    "store_id": "uuid"
  }
}
```

### POST /api/auth/refresh

- **Request:**

```json
{
  "refresh_token": "jwt_refresh_token"
}
```

- **Response:**

```json
{
  "access_token": "jwt_token"
}
```

## 2. User Management

### GET /api/users

- **Query Params:** `store_id`, `role`
- **Response:** List user dengan role dan toko.

### POST /api/users

- **Request Body:**

```json
{
  "username": "string",
  "password": "string",
  "role_id": "uuid",
  "store_id": "uuid"
}
```

- **Response:** User baru berhasil dibuat.

### PUT /api/users/:id

- **Request Body:** Update data user.
- **Response:** User berhasil diperbarui.

### DELETE /api/users/:id

- **Response:** User berhasil dihapus.

## 3. Store Management

### GET /api/stores

- **Response:** List semua toko.

### POST /api/stores

- **Request Body:** Tambah toko baru.

### PUT /api/stores/:id

- **Request Body:** Update data toko.

### DELETE /api/stores/:id

- **Response:** Toko berhasil dihapus.

## 4. Barang (Product)

### GET /api/products

- **Query Params:** `store_id`, `category_id`
- **Response:** List produk per toko.

### POST /api/products

- **Request Body:** Tambah produk baru.

### PUT /api/products/:id

- **Request Body:** Update produk.

### DELETE /api/products/:id

- **Response:** Produk berhasil dihapus.

## 5. Kategori Barang (Category)

CRUD endpoint mirip products.

## 6. Stok (Stock & Stock Movement)

### GET /api/stocks

- **Query Params:** `store_id`, `product_id`
- **Response:** Stok saat ini.

### POST /api/stocks/adjust

- **Request Body:** Penyesuaian stok.
- **Response:** Stok berhasil diperbarui.

### GET /api/stock-movements

- **Response:** Riwayat stok per toko.

## 7. Transaksi (Sales)

### GET /api/transactions

- **Query Params:** `store_id`, `date_from`, `date_to`

### POST /api/transactions

- **Request Body:** Input transaksi baru (items, qty, payment)
- **Response:** Transaksi berhasil dibuat, nomor invoice di-generate.

### GET /api/transactions/:id

- **Response:** Detail transaksi.

## 8. Laporan (Reports)

### GET /api/reports/sales

- **Query Params:** `store_id`, `date_from`, `date_to`, `kasir_id`
- **Response:** Data laporan, top produk, grafik.

### GET /api/reports/export

- **Query Params:** `store_id`, `date_from`, `date_to`
- **Response:** File Excel (.xlsx)

## 9. Backup & Restore

### POST /api/backup

- **Response:** File backup database.

### POST /api/restore

- **Request Body:** Upload file backup.
- **Response:** Database berhasil dikembalikan.

## 10. Activity Logs

### GET /api/activity-logs

- **Query Params:** `store_id`, `user_id`, `date_from`, `date_to`
- **Response:** Riwayat aktivitas user (login, transaksi, update stok, dll.)
