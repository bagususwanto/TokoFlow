# ⚙️ System Features - TokoFlow

Semua fitur dirancang agar **mudah digunakan**, **ringan di perangkat**, dan **siap dipakai tanpa instalasi tambahan**.  
Pengguna cukup **mendaftar akun** dan dapat langsung mengelola toko dari **HP**, **tablet**, atau **komputer**.

---

## 🧩 Modul Utama

Berikut adalah daftar modul fitur utama yang dikembangkan di **TokoFlow**, disusun sesuai prioritas implementasi.

### 1. 🔐 Autentikasi & Akses Pengguna (MVP)

| Fitur                 | Deskripsi                                    | Keterangan              |
| --------------------- | -------------------------------------------- | ----------------------- |
| **Login & Register**  | Pengguna dapat mendaftar dan masuk ke sistem | Dasar SaaS multi-tenant |
| **Token Akses (JWT)** | Sistem autentikasi aman berbasis token       | Otomatis login ulang    |
| **Role & Permission** | Hak akses Owner, Admin, dan Kasir            | Pengaturan peran toko   |
| **Logout**            | Hapus sesi login secara aman                 | -                       |

💡 _Fitur ini memastikan setiap toko dan pengguna memiliki data yang terpisah (multi-tenant)._

---

### 2. 🏬 Manajemen Pengguna & Toko

| Fitur                     | Deskripsi                              | Keterangan            |
| ------------------------- | -------------------------------------- | --------------------- |
| **Kelola Toko**           | Tambah dan atur cabang toko            | Mendukung multi-store |
| **Kelola Pengguna**       | Tambah user dengan peran tertentu      | Owner, Admin, Kasir   |
| **Atribusi User ke Toko** | Setiap user dikaitkan ke toko tertentu | Multi-user ready      |
| **Status Pengguna**       | Aktif / Nonaktif                       | Kontrol akses mudah   |

---

### 3. 📦 Manajemen Produk & Stok

| Fitur               | Deskripsi                    | Keterangan            |
| ------------------- | ---------------------------- | --------------------- |
| **Tambah Produk**   | Nama, SKU, harga beli & jual | Dukungan multi-satuan |
| **Kategori Barang** | Kelompokkan produk           | -                     |
| **Barcode**         | Dukungan scanner barcode     | Opsional              |
| **Status Produk**   | Aktif / Nonaktif             | -                     |
| **Laporan Stok**    | Lihat stok per toko          | Real-time             |

💡 _Fitur ini jadi dasar operasional toko untuk mencatat dan memantau stok secara otomatis._

---

### 4. 💰 Penjualan (Point of Sale / POS)

| Fitur                   | Deskripsi                               | Keterangan                                |
| ----------------------- | --------------------------------------- | ----------------------------------------- |
| **Pencarian Barang**    | Berdasarkan nama, SKU, atau barcode     | Cepat dan ringan                          |
| **Keranjang Penjualan** | Tambah / hapus produk sebelum transaksi | -                                         |
| **Hitung Otomatis**     | Subtotal dan total transaksi            | -                                         |
| **Pembayaran**          | Tunai / Transfer                        | -                                         |
| **Simpan Transaksi**    | Rekam transaksi ke database             | -                                         |
| **Cetak Struk**         | Cetak / unduh invoice penjualan         | Dukungan printer Bluetooth _(next phase)_ |

📱 _Kasir bisa melakukan transaksi langsung dari browser HP tanpa instalasi._

---

### 5. 📊 Laporan & Dashboard

| Fitur                 | Deskripsi                          | Keterangan      |
| --------------------- | ---------------------------------- | --------------- |
| **Ringkasan Harian**  | Tampilkan total penjualan harian   | Dashboard utama |
| **Laporan Bulanan**   | Analisis performa toko             | Grafik & tabel  |
| **Laporan Stok**      | Stok barang terkini                | -               |
| **Riwayat Transaksi** | Filter berdasarkan tanggal & kasir | -               |
| **Ekspor Excel**      | Unduh laporan ke Excel             | Fitur Premium   |

💡 _Membantu pemilik toko memantau performa bisnis secara real-time._

---

### 6. 🔁 Manajemen Stok Lanjutan (Phase 2)

| Fitur                     | Deskripsi                            | Keterangan        |
| ------------------------- | ------------------------------------ | ----------------- |
| **Transfer Antar Toko**   | Pindahkan stok antar cabang          | Untuk multi-store |
| **Penyesuaian Stok**      | Koreksi stok manual (+/-)            | -                 |
| **Log Pergerakan Barang** | Catatan otomatis setiap stok berubah | -                 |

---

### 7. 👥 Pelanggan & Supplier (Next Phase)

| Modul              | Fitur                                    | Keterangan              |
| ------------------ | ---------------------------------------- | ----------------------- |
| **Pelanggan**      | Simpan data pelanggan, riwayat pembelian | Loyalitas pelanggan     |
| **Supplier**       | Catat pemasok & riwayat pembelian        | Dasar untuk modul PO    |
| **Purchase Order** | Buat dan setujui permintaan pembelian    | Integrasi ke stok masuk |

---

### 8. 🧾 Audit Trail & Keamanan Data

| Fitur                 | Deskripsi                             | Keterangan         |
| --------------------- | ------------------------------------- | ------------------ |
| **Log Aktivitas**     | Lacak login/logout dan perubahan data | Transparansi penuh |
| **Riwayat Transaksi** | Pantau aktivitas kasir dan admin      | -                  |
| **Ekspor Log**        | Download riwayat aktivitas            | Fitur Premium      |

---

## 💸 Model Penggunaan & Paket

TokoFlow disediakan dengan model **langganan bulanan (SaaS)** agar semua data tersimpan aman di **cloud** dan bisa diakses kapan saja.

| Paket                | Harga (perkiraan) | Fitur                                                           |
| -------------------- | ----------------- | --------------------------------------------------------------- |
| **Starter (Gratis)** | Rp0               | 1 toko, 20 produk, laporan harian                               |
| **Basic**            | Rp49.000/bln      | 3 toko, laporan Excel, dashboard, role user                     |
| **Pro**              | Rp99.000/bln      | Tanpa batas toko, audit log, ekspor laporan, dukungan prioritas |

---

## ⚙️ Teknologi

- **Backend:** Node.js (Express) + Sequelize ORM
- **Database:** PostgreSQL _(Multi-tenant)_
- **Frontend:** React (Vite + Material-UI)
- **Autentikasi:** JWT
- **Hosting:** Cloud (Render / Railway / Vercel)
- **Payment Integration:** Midtrans / Xendit _(Subscription Billing)_

---

## 🧭 Tahapan Implementasi

| Tahap          | Fokus                                | Target                        |
| -------------- | ------------------------------------ | ----------------------------- |
| **MVP**        | Login, Produk, POS, Laporan dasar    | Rilis versi uji coba _(Beta)_ |
| **Phase 2**    | Multi toko, Transfer stok, Dashboard | Versi SaaS berbayar           |
| **Next Phase** | Pelanggan, Supplier, Purchase Order  | Versi Pro + Enterprise        |

---

📘 _Dokumen ini menjadi acuan pengembangan API dan UI Flow untuk versi SaaS **TokoFlow** yang ditujukan bagi UMKM retail dan toko kecil._
