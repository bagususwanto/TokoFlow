# ERD - TokoFlow

Dokumen ini menjelaskan **Entity Relationship Diagram (ERD)** sistem TokoFlow, mencakup modul utama: Users, Stores, Products, Inventory, Sales, dan Audit Trail.

---

## 1. Entities & Relationships

### 1.1 Users

| Column    | Type     | PK/FK/Notes                |
| --------- | -------- | -------------------------- |
| id        | UUID     | PK                         |
| username  | string   | unique                     |
| password  | string   | hashed                     |
| fullName  | string   | -                          |
| role      | enum     | owner/admin/kasir          |
| storeId   | UUID     | FK -> stores.id (nullable) |
| isActive  | boolean  | default true               |
| createdAt | datetime | -                          |
| updatedAt | datetime | -                          |

### 1.2 Stores

| Column    | Type     | PK/FK/Notes |
| --------- | -------- | ----------- |
| id        | UUID     | PK          |
| name      | string   | -           |
| address   | string   | -           |
| phone     | string   | optional    |
| createdAt | datetime | -           |
| updatedAt | datetime | -           |

### 1.3 Products

| Column     | Type     | PK/FK/Notes              |
| ---------- | -------- | ------------------------ |
| id         | UUID     | PK                       |
| sku        | string   | unique                   |
| name       | string   | -                        |
| categoryId | UUID     | FK -> categories.id/null |
| unit       | string   | pcs/box/pack             |
| costPrice  | number   | -                        |
| salePrice  | number   | -                        |
| barcode    | string   | optional                 |
| isActive   | boolean  | default true             |
| createdAt  | datetime | -                        |
| updatedAt  | datetime | -                        |

### 1.4 Inventory

| Column    | Type     | PK/FK/Notes       |
| --------- | -------- | ----------------- |
| id        | UUID     | PK                |
| storeId   | UUID     | FK -> stores.id   |
| productId | UUID     | FK -> products.id |
| type      | enum     | IN/OUT/ADJUST     |
| quantity  | number   | -                 |
| reason    | string   | optional          |
| reference | string   | optional          |
| createdAt | datetime | -                 |

### 1.5 Sales

| Column    | Type     | PK/FK/Notes     |
| --------- | -------- | --------------- |
| id        | UUID     | PK              |
| storeId   | UUID     | FK -> stores.id |
| userId    | UUID     | FK -> users.id  |
| total     | number   | -               |
| status    | enum     | SAVED/DRAFT     |
| notes     | string   | optional        |
| createdAt | datetime | -               |
| updatedAt | datetime | -               |

#### Sales Details

| Column    | Type   | PK/FK/Notes         |
| --------- | ------ | ------------------- |
| id        | UUID   | PK                  |
| saleId    | UUID   | FK -> sales.id      |
| productId | UUID   | FK -> products.id   |
| sku       | string | copied from product |
| name      | string | copied from product |
| unitPrice | number | -                   |
| quantity  | number | -                   |
| discount  | number | optional            |

### 1.6 Audit Trail

| Column    | Type     | PK/FK/Notes                       |
| --------- | -------- | --------------------------------- |
| id        | UUID     | PK                                |
| userId    | UUID     | FK -> users.id                    |
| module    | string   | PRODUCT/SALES/INVENTORY/AUTH      |
| action    | string   | CREATE/UPDATE/DELETE/LOGIN/LOGOUT |
| before    | JSON     | optional                          |
| after     | JSON     | optional                          |
| meta      | JSON     | ip, userAgent                     |
| createdAt | datetime | -                                 |

### 1.7 Categories

| Column    | Type     | PK/FK/Notes |
| --------- | -------- | ----------- |
| id        | UUID     | PK          |
| name      | string   | unique      |
| createdAt | datetime | -           |
| updatedAt | datetime | -           |

---

## 2. Relationships

- **Users -> Stores**: Many-to-One (user belongs to a store, owner may have null)
- **Products -> Categories**: Many-to-One (product belongs to category)
- **Inventory -> Stores & Products**: Many-to-One (movement per store & product)
- **Sales -> Stores & Users**: Many-to-One (sales belongs to store & created by user)
- **SalesDetails -> Sales & Products**: Many-to-One
- **Audit -> Users**: Many-to-One

---

Diagram ERD bisa divisualisasikan menggunakan tool seperti draw.io berdasarkan tabel dan relasi di atas.
