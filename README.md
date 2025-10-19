# Sistem Kasir & Stok - Multi Toko

## 📌 Deskripsi

Sistem ini adalah aplikasi Point of Sale (POS) berbasis web yang mendukung multi-cabang toko dengan manajemen stok, transaksi penjualan, dan laporan real-time. Sistem dirancang untuk usaha retail/minimarket agar operasional lebih efisien, akurat, dan terkontrol.

## ⚡ Fitur Utama

- Manajemen barang & kategori
- Stok barang per toko dengan notifikasi minimal stock
- Transaksi kasir (POS) + cetak struk
- Multi-toko & role-based access (Owner, Admin, Kasir)
- Laporan penjualan harian, mingguan, bulanan
- Backup & restore database
- Activity logs / audit trail

## 🧰 Tech Stack

- **Frontend:** React.js, Material-UI, MUI Charts
- **Backend:** Node.js, Express.js, Sequelize
- **Database:** PostgreSQL
- **Authentication:** JWT
- **DevOps / Deployment:** GitHub, Render, dotenv
- **Testing:** Jest, React Testing Library, Supertest

## 📂 Struktur Folder

- `/frontend` - Source code frontend React
- `/backend` - Source code backend Express & Sequelize
- `/doc` - Dokumentasi sistem (Overview, Features, Use Case, ERD, API Spec, Tech Stack, Roadmap)

## 📚 Dokumentasi

Untuk dokumentasi lengkap, lihat folder [doc](./doc) atau buka GitHub Pages dari folder tersebut.

## 🚀 Deployment

1. Setup database (PostgreSQL)
2. Set environment variables di `.env`
3. Jalankan backend: `npm install && npm start` di folder `/backend`
4. Build frontend: `npm install && npm run build` di folder `/frontend` → deploy ke Render Static Site atau server pilihan
5. Integrasi backend & frontend sesuai environment

## 👨‍💻 Kontributor

- Bagus Uswanto (Developer)

## 📄 Lisensi

Lisensi **Proprietary (Non-Free)** © 2025
Seluruh kode dan dokumentasi tidak boleh digunakan, dimodifikasi, atau disebarkan tanpa izin tertulis dari pemilik proyek.
