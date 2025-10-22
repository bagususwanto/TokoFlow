# 🏪 TokoFlow Project

TokoFlow adalah aplikasi kasir dan manajemen stok berbasis **SaaS (Software as a Service)** yang dirancang untuk membantu **UMKM dan bisnis retail multi-cabang**. Sistem ini mendukung **multi-store**, **multi-user**, dan **pelaporan real-time** untuk mempermudah operasional bisnis.

---

## 📁 Struktur Project

```
root/
│
├─ frontend/        # Source code frontend (React + Material-UI + Vite)
├─ backend/         # Source code backend (Node.js + Express + Sequelize)
├─ docs/            # Dokumentasi teknis sistem
│   ├─ overview.md          # Ringkasan sistem & ruang lingkup
│   ├─ features.md          # Daftar fitur utama & dependency antar modul
│   ├─ ui-flow.md           # Alur navigasi user & proses onboarding
│   ├─ erd.md               # Skema database (ERD & DBML)
│   ├─ api-spec.md          # Spesifikasi API dengan contoh request/response
│   └─ use-case.md          # Use case lengkap per role (Owner, Admin, Kasir)
├─ postman/         # Koleksi API testing (Postman Collection)
├─ README.md        # Dokumentasi utama proyek (root)
└─ LICENSE          # Lisensi proyek
```

---

## ⚙️ Teknologi yang Digunakan

| Layer       | Teknologi                               |
| ----------- | --------------------------------------- |
| Frontend    | React + Material UI + Vite              |
| Backend     | Node.js (Express) + Sequelize ORM       |
| Database    | PostgreSQL                              |
| Autentikasi | JWT (Access & Refresh Token)            |
| Infra (Dev) | GitHub Pages (docs), Postman (API test) |

---

## 🚀 Cara Menjalankan Proyek

### 🧩 Backend (API Server)

```bash
cd backend
npm install
npm run dev
# Akses: http://localhost:5000/api/v1
```

### 💻 Frontend (Web Client)

```bash
cd frontend
npm install
npm run dev
# Akses: http://localhost:5173
```

---

## 🧭 Alur Onboarding (Tenant Baru)

1. Owner mendaftar akun pertama melalui halaman registrasi
2. Sistem otomatis membuat:

   - Toko pertama (default store)
   - User kasir awal (default cashier)

3. Setelah login, Owner diarahkan ke **Dashboard Setup Guide** untuk:

   - Menambah produk pertama
   - Melengkapi informasi toko
   - Menambah admin atau kasir tambahan

4. Sistem siap digunakan untuk transaksi dan pelaporan real-time

---

## 📚 Dokumentasi Lengkap

Semua dokumentasi berada di folder `/docs`:

| File        | Deskripsi                                             |
| ----------- | ----------------------------------------------------- |
| overview.md | Ringkasan sistem & ruang lingkup SaaS                 |
| features.md | Modul utama & dependency antar fitur                  |
| ui-flow.md  | Alur navigasi pengguna & onboarding flow              |
| erd.md      | Entity Relationship Diagram (ERD) & struktur database |
| api-spec.md | Spesifikasi endpoint API                              |
| use-case.md | Daftar use case per role                              |

📖 Versi web dokumentasi tersedia di:
➡️ [https://bagususwanto.github.io/TokoFlow/](https://bagususwanto.github.io/TokoFlow/)

---

## 🧪 Testing API (Postman)

Gunakan koleksi Postman yang tersedia di folder `/postman`:

1. Import `TokoFlow-Complete.postman_collection.json`
2. Import `TokoFlow.postman_environment.json`
3. Login via `POST /auth/login` untuk mendapatkan token JWT
4. Semua request selanjutnya otomatis memakai `{{token}}`

---

## 👥 Kontributor

| Nama          | Peran                                |
| ------------- | ------------------------------------ |
| Bagus Uswanto | Fullstack Developer / Project Author |

---

## 📄 Lisensi

Proyek ini menggunakan lisensi **MIT License**.

© 2025 Bagus Uswanto. Semua hak cipta dilindungi.

---

## 🏁 Status Proyek

| Atribut         | Status                                 |
| --------------- | -------------------------------------- |
| Versi           | v1.0.0 - SaaS Multi-Store Edition      |
| Status          | Development                            |
| Target Pengguna | UMKM, Retail, Minimarket, Multi-Cabang |
