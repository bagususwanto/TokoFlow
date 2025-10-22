# 🧭 UI Flow – TokoFlow

Dokumen ini menjelaskan alur navigasi pengguna (**user flow**) pada sistem **TokoFlow SaaS**, aplikasi manajemen **penjualan & stok berbasis cloud** untuk UMKM.  
Fokus utama mencakup **alur onboarding**, **penggunaan harian (POS, stok, laporan)**, serta **manajemen toko dan user**.

---

## 🌐 1. Global Navigation Structure

| Menu Utama                   | Deskripsi                            |
| ---------------------------- | ------------------------------------ |
| **Dashboard**                | Ringkasan penjualan dan stok terkini |
| **POS (Kasir)**              | Transaksi penjualan cepat            |
| **Produk**                   | Manajemen daftar produk dan harga    |
| **Stok**                     | Monitoring dan mutasi stok per toko  |
| **Laporan**                  | Ringkasan penjualan dan stok         |
| **User & Role**              | Kelola pengguna dan hak akses        |
| **Toko (Store)**             | Tambah atau ubah cabang              |
| **Audit Trail**              | Riwayat aktivitas pengguna           |
| **Profil / Pengaturan Akun** | Kelola akun, langganan, dan logout   |

---

## 🚀 2. Onboarding Flow (First-Time User)

| Step | Halaman / Aksi                | Keterangan                                               |
| ---- | ----------------------------- | -------------------------------------------------------- |
| 1    | Landing Page / Daftar Akun    | Pengguna mendaftar dengan email, nama toko, dan password |
| 2    | Verifikasi Email _(opsional)_ | Konfirmasi untuk aktivasi akun                           |
| 3    | Setup Awal Toko               | Isi nama toko, alamat, dan kategori usaha                |
| 4    | Tambah Produk Pertama         | Minimal 1 produk untuk mulai transaksi                   |
| 5    | Mulai POS / Dashboard         | Sistem otomatis menampilkan ringkasan toko               |

💡 _Tujuan onboarding: pengguna bisa mulai jualan dalam waktu < 5 menit._

---

## 🔐 3. Authentication & Session Flow

| Step | Aksi                       | Kondisi                                    |
| ---- | -------------------------- | ------------------------------------------ |
| 1    | User membuka halaman Login | -                                          |
| 2    | Input email & password     | Validasi frontend                          |
| 3    | Klik “Masuk”               | `POST /auth/login`                         |
| 4    | Jika berhasil              | Simpan token JWT + refresh                 |
| 5    | Redirect ke Dashboard      | -                                          |
| 6    | Jika gagal                 | Tampilkan pesan error                      |
| 7    | Jika token expired         | Auto refresh, jika gagal → Logout otomatis |

---

## 📊 4. Dashboard Flow

| Step | Halaman / Aksi                     | Keterangan                                              |
| ---- | ---------------------------------- | ------------------------------------------------------- |
| 1    | User masuk ke Dashboard            | Setelah login                                           |
| 2    | Lihat ringkasan penjualan hari ini | Total transaksi, omzet, stok rendah                     |
| 3    | Navigasi cepat                     | Tombol “Mulai Jualan”, “Tambah Produk”, “Lihat Laporan” |
| 4    | Notifikasi stok menipis            | Pop-up otomatis atau badge merah                        |

💡 _Dashboard berfungsi sebagai pusat kontrol untuk pemilik toko._

---

## 💰 5. POS (Point of Sale) Flow

| Step | Halaman / Aksi               | Keterangan                                 |
| ---- | ---------------------------- | ------------------------------------------ |
| 1    | Masuk ke halaman POS         | User (kasir) otomatis terhubung ke tokonya |
| 2    | Cari produk                  | Berdasarkan nama, SKU, atau barcode        |
| 3    | Tambahkan ke keranjang       | Klik “Tambah” atau scan barcode            |
| 4    | Ubah kuantitas / hapus item  | -                                          |
| 5    | Sistem hitung total otomatis | Subtotal, diskon, total bayar              |
| 6    | Pilih metode pembayaran      | Tunai / Transfer                           |
| 7    | Klik “Simpan Transaksi”      | `POST /sales`                              |
| 8    | Cetak / kirim struk digital  | Struk PDF atau WhatsApp                    |
| 9    | Stok otomatis berkurang      | Update ke database                         |

📱 _Tampilan POS responsif untuk HP, dengan tombol besar dan navigasi cepat._

---

## 📦 6. Manajemen Produk Flow

| Step | Halaman / Aksi               | Keterangan                            |
| ---- | ---------------------------- | ------------------------------------- |
| 1    | Buka menu “Produk”           | Menampilkan daftar produk             |
| 2    | Klik “Tambah Produk”         | Nama, SKU, kategori, harga, stok awal |
| 3    | Simpan produk                | `POST /products`                      |
| 4    | Edit atau Nonaktifkan produk | `PUT /products/:id`                   |
| 5    | Filter dan cari produk       | Berdasarkan kategori atau status      |

💡 _Formulir dibuat sesederhana mungkin untuk pengguna non-teknis._

---

## 📈 7. Manajemen Stok Flow

| Step | Halaman / Aksi                     | Keterangan                        |
| ---- | ---------------------------------- | --------------------------------- |
| 1    | Buka menu “Stok”                   | Lihat stok per toko               |
| 2    | Klik “Mutasi Stok”                 | Stock In / Stock Out / Adjustment |
| 3    | Pilih produk dan qty               | Validasi form                     |
| 4    | Simpan                             | `POST /inventory`                 |
| 5    | Sistem otomatis mencatat log       | Ledger & audit trail              |
| 6    | _(Next Phase)_ Transfer antar toko | `POST /inventory/transfer`        |

---

## 👥 8. Manajemen Pengguna & Role Flow

| Step | Halaman / Aksi            | Keterangan                |
| ---- | ------------------------- | ------------------------- |
| 1    | Buka menu “User & Role”   | Hanya untuk Owner / Admin |
| 2    | Tambah pengguna           | Nama, username, role      |
| 3    | Assign role & toko        | Owner, Admin, Kasir       |
| 4    | Simpan                    | `POST /users`             |
| 5    | Aktif / Nonaktif pengguna | -                         |

---

## 🏬 9. Manajemen Toko Flow

| Step | Halaman / Aksi | Keterangan |
| ---- | -------------- | ---------- |
| 1    | Buka menu      |
