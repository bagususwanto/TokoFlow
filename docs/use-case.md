# Use Case - TokoFlow

Dokumen ini menjelaskan interaksi utama antara user dengan sistem TokoFlow (MVP).

---

## 1. Actors

| Actor | Deskripsi                                               |
| ----- | ------------------------------------------------------- |
| Owner | Mengelola seluruh toko, melihat laporan, manajemen user |
| Admin | Mengelola produk, stok, laporan toko tertentu           |
| Kasir | Melakukan transaksi penjualan di POS                    |

---

## 2. Use Cases Utama

| Use Case             | Actor             | Deskripsi                                                                      |
| -------------------- | ----------------- | ------------------------------------------------------------------------------ |
| Login                | Owner/Admin/Kasir | User masuk ke sistem menggunakan username/password, mendapat JWT token         |
| Dashboard            | Owner/Admin       | Melihat ringkasan penjualan, stok rendah, dan quick action                     |
| Manage Users         | Owner/Admin       | Tambah, edit, assign role, assign toko, deactivate user                        |
| Manage Stores        | Owner             | CRUD data toko dan assign user ke toko                                         |
| Manage Products      | Admin             | CRUD produk, atur kategori, harga, barcode, status aktif                       |
| Inventory Management | Admin             | Stock In/Out/Adjustment, monitoring stok per toko                              |
| POS Transaction      | Kasir             | Cari produk, add to cart, input qty, pembayaran, simpan transaksi, cetak struk |
| Reports              | Owner/Admin       | Lihat laporan harian/bulanan, stock report, stock movement                     |
| Audit Trail          | Owner/Admin       | Monitor user activity, data change, stock mutation, transaction log            |

---

## 3. Singkat Alur Interaksi per Actor

### 3.1 Owner

1. Login -> Dashboard -> Manage Users / Stores -> Reports / Audit Trail

### 3.2 Admin

1. Login -> Dashboard -> Manage Products -> Inventory -> Reports

### 3.3 Kasir

1. Login -> POS -> Cari produk -> Add to Cart -> Input Qty -> Payment -> Save Transaction -> Print Receipt

---

Dokumen ini versi singkat untuk cepat memahami **siapa melakukan apa** di sistem TokoFlow dan bisa langsung dipakai sebagai referensi implementasi frontend & backend.
