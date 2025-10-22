# Overview - TokoFlow

## Ringkasan

TokoFlow adalah aplikasi yang dirancang untuk membantu proses penjualan, manajemen stok, dan pengelolaan transaksi pada bisnis yang memiliki lebih dari satu toko. Sistem ini mendukung pencatatan penjualan secara real-time, pengecekan stok antar toko, serta laporan transaksi untuk mendukung pengambilan keputusan.

## Tujuan Sistem

- Mempermudah pencatatan penjualan dan pergerakan stok barang.
- Mengurangi kesalahan pencatatan manual.
- Mempercepat proses transaksi kasir.
- Menyediakan laporan penjualan dan stok yang akurat.
- Mendukung kolaborasi antar user dengan role berbeda.

## Ruang Lingkup

Sistem ini mencakup fitur utama:

- Multi-user & Multi-store
- Manajemen Produk & Kategori
- Manajemen Stok & Transfer Stok antar Toko
- Point of Sales (POS)
- Manajemen Pelanggan **(Next Phase)**
- Manajemen Supplier **(Next Phase)**
- Purchase Order **(Next Phase)**
- Laporan Penjualan
- Riwayat Aktivitas
- Hak Akses & Role Management

## Peran Pengguna

| Role  | Deskripsi                                    |
| ----- | -------------------------------------------- |
| Owner | Melihat laporan seluruh toko, mengelola user |
| Admin | Mengelola produk, stok, dan laporan toko     |
| Kasir | Melakukan transaksi penjualan                |

## Fitur Utama

- Login & Autentikasi (JWT + Role Based Access Control)
- Multi Store Management
- Manajemen Produk & Stok
- Penjualan (Point of Sale / POS)
- Dashboard Penjualan & Notifikasi Stok
- Riwayat Transaksi & Audit Log
- Laporan Penjualan & Stok

## Teknologi

Sistem ini dikembangkan menggunakan stack modern:

- Backend: Node.js (Express) + Sequelize ORM
- Database: PostgreSQL
- Frontend: React + Material-UI
- Autentikasi: JWT

---

Dokumen ini berfungsi sebagai gambaran awal sistem dan menjadi referensi utama dalam pengembangan.
