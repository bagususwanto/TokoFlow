# 🧱 ERD – TokoFlow

## 1. 📘 Ringkasan

**Entity Relationship Diagram (ERD)** TokoFlow menggambarkan struktur database untuk sistem manajemen toko berbasis **Software as a Service (SaaS)**.  
Setiap akun pengguna (**owner**) memiliki satu atau lebih **toko (store)** dalam satu lingkungan cloud (_multi-tenant_).  
Semua data **penjualan**, **stok**, dan **user** disimpan **terisolasi per toko** untuk menjaga keamanan dan privasi data antar pengguna.

---

## 2. 📂 Daftar Entitas & Relasi

### 2.1 👤 Users

| Kolom          | Tipe            | Keterangan                              |
| -------------- | --------------- | --------------------------------------- |
| `id`           | UUID            | Primary key                             |
| `fullName`     | string          | Nama lengkap                            |
| `email`        | string          | Unik, digunakan untuk login             |
| `passwordHash` | string          | Disimpan dalam bentuk hash              |
| `role`         | enum            | owner / admin / kasir                   |
| `storeId`      | UUID (nullable) | FK → `stores.id` (user terikat ke toko) |
| `planId`       | UUID (nullable) | FK → `subscription_plans.id`            |
| `isActive`     | boolean         | Default: true                           |
| `createdAt`    | datetime        | -                                       |
| `updatedAt`    | datetime        | -                                       |

💡 _Owner dapat memiliki banyak toko (multi-store), sementara admin dan kasir hanya terikat ke satu toko._

---

### 2.2 🏬 Stores

| Kolom       | Tipe     | Keterangan      |
| ----------- | -------- | --------------- |
| `id`        | UUID     | Primary key     |
| `ownerId`   | UUID     | FK → `users.id` |
| `name`      | string   | Nama toko       |
| `address`   | string   | Alamat toko     |
| `phone`     | string   | Opsional        |
| `isActive`  | boolean  | Default: true   |
| `createdAt` | datetime | -               |
| `updatedAt` | datetime | -               |

🔗 **Relasi:**

- Users (owner) → Stores _(one-to-many)_
- Stores → Products, Sales, Inventory _(one-to-many)_

---

### 2.3 🗂️ Categories

| Kolom       | Tipe     | Keterangan       |
| ----------- | -------- | ---------------- |
| `id`        | UUID     | Primary key      |
| `storeId`   | UUID     | FK → `stores.id` |
| `name`      | string   | Unik per toko    |
| `createdAt` | datetime | -                |
| `updatedAt` | datetime | -                |

---

### 2.4 📦 Products

| Kolom        | Tipe            | Keterangan           |
| ------------ | --------------- | -------------------- |
| `id`         | UUID            | Primary key          |
| `storeId`    | UUID            | FK → `stores.id`     |
| `sku`        | string          | Unik per toko        |
| `name`       | string          | Nama produk          |
| `categoryId` | UUID (nullable) | FK → `categories.id` |
| `unit`       | string          | pcs / box / pack     |
| `costPrice`  | decimal         | Harga modal          |
| `salePrice`  | decimal         | Harga jual           |
| `barcode`    | string          | Opsional             |
| `isActive`   | boolean         | Default: true        |
| `createdAt`  | datetime        | -                    |
| `updatedAt`  | datetime        | -                    |

---

### 2.5 📈 Inventory (Mutasi Stok)

| Kolom       | Tipe     | Keterangan                    |
| ----------- | -------- | ----------------------------- |
| `id`        | UUID     | Primary key                   |
| `storeId`   | UUID     | FK → `stores.id`              |
| `productId` | UUID     | FK → `products.id`            |
| `type`      | enum     | IN / OUT / ADJUST / TRANSFER  |
| `quantity`  | integer  | Jumlah stok berubah           |
| `reference` | string   | Referensi transaksi / dokumen |
| `reason`    | string   | Keterangan opsional           |
| `createdBy` | UUID     | FK → `users.id`               |
| `createdAt` | datetime | -                             |

---

### 2.6 💰 Sales (Transaksi Penjualan)

| Kolom           | Tipe            | Keterangan                    |
| --------------- | --------------- | ----------------------------- |
| `id`            | UUID            | Primary key                   |
| `storeId`       | UUID            | FK → `stores.id`              |
| `userId`        | UUID            | FK → `users.id` (kasir/admin) |
| `customerId`    | UUID (nullable) | FK → `customers.id`           |
| `total`         | decimal         | Total transaksi               |
| `paymentMethod` | enum            | cash / transfer / qris        |
| `status`        | enum            | SAVED / DRAFT / CANCELLED     |
| `notes`         | string          | Opsional                      |
| `createdAt`     | datetime        | -                             |
| `updatedAt`     | datetime        | -                             |

---

### 2.7 🧾 Sales Details

| Kolom       | Tipe    | Keterangan                        |
| ----------- | ------- | --------------------------------- |
| `id`        | UUID    | Primary key                       |
| `saleId`    | UUID    | FK → `sales.id`                   |
| `productId` | UUID    | FK → `products.id`                |
| `sku`       | string  | Duplikat dari produk              |
| `name`      | string  | Duplikat dari produk              |
| `quantity`  | integer | Jumlah barang                     |
| `unitPrice` | decimal | Harga per item                    |
| `discount`  | decimal | Opsional                          |
| `total`     | decimal | (quantity × unitPrice) - discount |

---

### 2.8 🔍 Audit Trail

| Kolom       | Tipe     | Keterangan                         |
| ----------- | -------- | ---------------------------------- |
| `id`        | UUID     | Primary key                        |
| `userId`    | UUID     | FK → `users.id`                    |
| `module`    | string   | PRODUCT / SALES / INVENTORY / AUTH |
| `action`    | string   | CREATE / UPDATE / DELETE / LOGIN   |
| `before`    | JSON     | Data sebelum perubahan             |
| `after`     | JSON     | Data sesudah perubahan             |
| `meta`      | JSON     | IP, userAgent                      |
| `createdAt` | datetime | -                                  |

---

### 2.9 💳 Subscription Plans _(SaaS Specific)_

| Kolom          | Tipe     | Keterangan                    |
| -------------- | -------- | ----------------------------- |
| `id`           | UUID     | Primary key                   |
| `name`         | string   | Nama paket (Free, Basic, Pro) |
| `price`        | decimal  | Harga per bulan               |
| `storeLimit`   | integer  | Jumlah toko maksimum          |
| `productLimit` | integer  | Jumlah produk maksimum        |
| `userLimit`    | integer  | Jumlah user maksimum          |
| `features`     | JSON     | Daftar fitur aktif            |
| `createdAt`    | datetime | -                             |

---

### 2.10 📆 Subscriptions

| Kolom              | Tipe     | Keterangan                   |
| ------------------ | -------- | ---------------------------- |
| `id`               | UUID     | Primary key                  |
| `userId`           | UUID     | FK → `users.id` (owner)      |
| `planId`           | UUID     | FK → `subscription_plans.id` |
| `status`           | enum     | ACTIVE / EXPIRED / CANCELLED |
| `startDate`        | datetime | -                            |
| `endDate`          | datetime | -                            |
| `paymentReference` | string   | ID dari Midtrans / Xendit    |
| `createdAt`        | datetime | -                            |

---

## 3. 🔗 Hubungan Antar Entitas (Ringkasan)

| Relasi                    | Jenis       | Deskripsi                                  |
| ------------------------- | ----------- | ------------------------------------------ |
| Users ↔ Stores            | One-to-Many | Owner bisa punya banyak toko               |
| Stores ↔ Products         | One-to-Many | Tiap toko punya daftar produk sendiri      |
| Products ↔ Inventory      | One-to-Many | Setiap produk memiliki mutasi stok         |
| Sales ↔ SalesDetails      | One-to-Many | Setiap transaksi punya banyak item         |
| Sales ↔ Users             | Many-to-One | Transaksi dilakukan oleh kasir/admin       |
| Users ↔ SubscriptionPlans | Many-to-One | Tiap owner terikat ke satu paket langganan |
| AuditTrail ↔ Users        | Many-to-One | Log aktivitas oleh user tertentu           |

---

## 4. 🏗️ Model Multi-Tenant

TokoFlow menggunakan pendekatan **single database**, _isolated by `storeId`_:

- Semua tabel utama (`products`, `sales`, `inventory`, dll.) memiliki kolom `storeId`.
- Setiap pengguna (admin/kasir) hanya dapat mengakses data yang terkait dengan `storeId` mereka.
- Owner dapat melihat data lintas toko.

**Keuntungan:**

- ⚡ Skalabilitas tinggi (1 database untuk banyak tenant)
- 💾 Hemat resource (dibanding 1 DB per toko)
- 🔧 Mudah dikelola & di-backup

---

## 5. 🧠 Catatan Implementasi

- **ORM:** Sequelize (Node.js)
- **Database:** PostgreSQL
- **Schema:** Public, dengan `storeId` sebagai foreign key di semua entitas operasional
- **Autentikasi:** JWT + Role-Based Access Control
- **Integrasi Pembayaran:** Midtrans / Xendit _(Subscription Billing)_

---

📘 _ERD ini dirancang agar fleksibel dan siap dikembangkan sebagai sistem SaaS multi-tenant dengan opsi langganan (freemium → premium)._  
Struktur ini menjaga keseimbangan antara **skalabilitas**, **performa**, dan **kemudahan pengembangan backend** menggunakan **Express + Sequelize + PostgreSQL**.
