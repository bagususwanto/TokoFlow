# 🧱 Instalasi & Konfigurasi

Panduan ini menjelaskan cara menjalankan **Sistem Kasir & Stok Toko Kecil** secara lokal dan persiapan sebelum di-deploy ke **Render**.

---

## ⚙️ Prasyarat

Pastikan perangkat kamu sudah terpasang:

- **Node.js** v18 atau lebih baru
- **PostgreSQL** v14 atau lebih baru
- **Git**
- **VS Code** atau editor lain
- Akun **Render.com** (gratis)

---

## 📦 1. Clone Repository

```bash
git clone https://github.com/bagususwanto/store-pos.git
cd store-pos
```

---

## 🗃️ 2. Instal Dependensi

**Backend**

```bash
cd backend
npm install
```

**Frontend**

```bash
cd ../frontend
npm install
```

---

## ⚙️ 3. Konfigurasi Environment

**Backend**
Buat file .env di folder backend/ dan isi dengan:

```bash
PORT=5000
DB_HOST=localhost
DB_PORT=5432
DB_USER=postgres
DB_PASS=yourpassword
DB_NAME=store_pos_db
JWT_SECRET=secretkey123
```

**Frontend**
Buat file .env di folder frontend/ dan isi dengan:

```bash
VITE_API_URL=http://localhost:5000
```

---

## 🧰 4. Inisialisasi Database

Masuk ke PostgreSQL dan buat database baru:

```bash
CREATE DATABASE store_pos_db;
```

Kemudian jalankan migrasi (jika tersedia di backend):

```bash
npm run migrate
```

---

## ▶️ 5. Jalankan Aplikasi Secara Lokal

**Jalankan Backend**

```bash
cd backend
npm run dev
```

API akan berjalan di: http://localhost:5000

**Jalankan Frontend**

```bash
cd ../frontend
npm run dev
```

Frontend akan berjalan di: http://localhost:5173
