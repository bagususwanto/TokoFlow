# Use Case - TokoFlow

## 1. Aktor Sistem

| Actor | Deskripsi                                                                                                                           |
| ----- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Owner | Pemilik bisnis atau tenant utama yang mendaftar di sistem TokoFlow. Memiliki hak penuh untuk mengelola toko, pengguna, dan laporan. |
| Admin | Pengelola toko tertentu yang bertanggung jawab terhadap produk, stok, dan laporan transaksi di toko yang ditugaskan.                |
| Kasir | Pengguna operasional toko yang menjalankan transaksi penjualan harian di Point of Sale (POS).                                       |

## 2. Use Cases Utama

| Use Case                          | Actor        | Deskripsi                                                                                                                        |
| --------------------------------- | ------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| Registrasi & Onboarding Awal      | Owner        | Owner mendaftar akun baru di TokoFlow, lalu menjalani proses onboarding untuk membuat toko pertama, produk awal, dan user kasir. |
| Login & Autentikasi               | Semua        | Pengguna masuk menggunakan username & password, sistem memberikan JWT access token dan refresh token.                            |
| Dashboard Penjualan               | Owner, Admin | Menampilkan ringkasan penjualan, stok menipis, performa cabang, dan navigasi cepat ke fitur utama.                               |
| Manajemen User                    | Owner        | Menambah, mengubah, menonaktifkan user serta menetapkan role (Admin/Kasir) dan toko masing-masing.                               |
| Manajemen Toko (Store Management) | Owner        | Membuat cabang baru, memperbarui informasi toko, dan menugaskan user ke cabang.                                                  |
| Manajemen Produk                  | Admin        | Menambah, mengedit, atau menonaktifkan produk; mengatur kategori, harga, satuan, dan barcode.                                    |
| Manajemen Stok (Inventory)        | Admin        | Melakukan input stok awal, mutasi stok masuk/keluar, serta adjustment. Sistem otomatis merekam log stok.                         |
| Transaksi Penjualan (POS)         | Kasir        | Melakukan transaksi penjualan, memilih produk, memasukkan jumlah, menerima pembayaran, menyimpan transaksi, dan mencetak struk.  |
| Laporan & Analitik                | Owner, Admin | Melihat laporan penjualan harian/bulanan, stok per toko, pergerakan stok, dan performa cabang.                                   |
| Audit Trail                       | Owner, Admin | Memonitor semua aktivitas sistem: login, perubahan data, transaksi, dan pergerakan stok.                                         |

## 3. Alur Interaksi per Aktor

### 🧾 Owner (Tenant Utama)

Registrasi → Onboarding (Setup Toko & User Pertama) → Dashboard → Kelola Produk & User → Pantau Laporan → Audit Aktivitas

- Melalui onboarding, Owner langsung membuat toko pertama dan user kasir default.
- Bisa menambah cabang dan pengguna baru kapan saja.
- Melihat performa seluruh toko secara real-time di dashboard.

### 🏬 Admin (Pengelola Toko)

Login → Dashboard → Kelola Produk → Atur Stok → Lihat Laporan Toko

- Mengatur produk, stok, dan memantau transaksi toko yang ditugaskan.
- Melakukan stok in/out serta adjustment.
- Bisa ekspor laporan ke Excel untuk kebutuhan internal toko.

### 💵 Kasir (Penjualan)

Login → POS → Cari Produk → Tambah ke Keranjang → Pembayaran → Simpan Transaksi → Cetak Struk

- Fokus pada transaksi cepat dan mudah.
- Stok berkurang otomatis setelah transaksi berhasil.
- Struk dapat dicetak atau dikirim digital (PDF).

## 4. Use Case Tambahan (SaaS-Specific)

| Use Case                           | Actor  | Deskripsi                                                                                      |
| ---------------------------------- | ------ | ---------------------------------------------------------------------------------------------- |
| Manajemen Langganan (Subscription) | Owner  | Mengatur paket SaaS (Gratis / Pro / Enterprise) dan pembayaran berlangganan.                   |
| Multi-Tenant Isolation             | Sistem | Memastikan setiap tenant (owner) dan tokonya terisolasi secara data dan autentikasi.           |
| Notifikasi Sistem                  | Semua  | Mengirimkan notifikasi stok menipis, transaksi sukses, dan pembaruan sistem melalui dashboard. |

## 5. Catatan Implementasi

- Sistem menggunakan Role-Based Access Control (RBAC) untuk membedakan hak akses.
- Semua aktivitas penting dicatat di modul Audit Trail untuk kebutuhan pelacakan.
- Proses onboarding membantu pengguna baru memahami sistem tanpa perlu pelatihan khusus.
- Setiap tenant (owner) memiliki ruang data terpisah (multi-tenant structure).
- Semua data transaksi, stok, dan user antar toko bersifat real-time sync.
