# UI Flow - TokoFlow

Dokumen ini menjelaskan alur navigasi (user flow) pada sistem **TokoFlow** berdasarkan modul yang telah didefinisikan. Fokus utama dokumen ini adalah **MVP (Minimum Viable Product)** untuk mempermudah pengembangan sistem secara bertahap.

---

## 1. Global Navigation Structure (MVP)

| Menu Utama  | Deskripsi                                        |
| ----------- | ------------------------------------------------ |
| Login       | Autentikasi user menggunakan username & password |
| Dashboard   | Ringkasan penjualan dan stok per toko            |
| POS         | Transaksi penjualan (kasir)                      |
| Produk      | Manajemen daftar produk                          |
| Stok        | Monitoring & mutasi stok                         |
| Users       | Manajemen user dan role                          |
| Stores      | Manajemen cabang/toko                            |
| Audit Trail | Log aktivitas sistem                             |
| Logout      | Keluar dari sistem                               |

---

## 2. Authentication Flow (Login + Session)

| Step | Halaman/Action                  | Kondisi                       |
| ---- | ------------------------------- | ----------------------------- |
| 1    | User membuka halaman Login      | -                             |
| 2    | Input username dan password     | Validasi frontend             |
| 3    | Klik tombol Login               | -                             |
| 4    | Sistem kirim request ke backend | POST /auth/login              |
| 5    | Jika berhasil                   | Simpan access + refresh token |
| 6    | Redirect ke Dashboard           | -                             |
| 7    | Jika gagal                      | Tampilkan pesan error         |

**Session Handling**

| Kondisi       | Behavior           |
| ------------- | ------------------ |
| Token expired | Auto refresh token |
| Refresh gagal | Redirect ke Login  |

---

## 3. Dashboard Flow (Owner/Admin/Kasir)

| Step | Halaman/Action      | Keterangan                                 |
| ---- | ------------------- | ------------------------------------------ |
| 1    | Redirect dari Login | Setelah autentikasi sukses                 |
| 2    | Tampilkan ringkasan | Penjualan hari ini, transaksi, stok rendah |
| 3    | Aksi cepat          | Navigasi ke POS, Produk, Stok              |

---

## 4. POS Flow (Point of Sale)

| Step | Halaman/Action   | Keterangan                         |
| ---- | ---------------- | ---------------------------------- |
| 1    | Masuk ke POS     | User otomatis terikat ke store-nya |
| 2    | Cari produk      | Search by nama/SKU/barcode         |
| 3    | Tambah ke cart   | Klik tombol "Tambah"               |
| 4    | Edit kuantitas   | Input manual qty                   |
| 5    | Input pembayaran | Cash / Transfer                    |
| 6    | Simpan transaksi | POST /sales                        |
| 7    | Cetak struk      | Optional                           |

---

## 5. Product Management Flow

| Step | Halaman/Action      | Keterangan                 |
| ---- | ------------------- | -------------------------- |
| 1    | Buka halaman Produk | Dari menu sidebar          |
| 2    | Tambah Produk       | Nama, SKU, Kategori, Harga |
| 3    | Validasi form       | SKU unik                   |
| 4    | Simpan              | POST /products             |
| 5    | Edit produk         | PUT /products/:id          |
| 6    | Nonaktifkan produk  | Status aktif/nonaktif      |

---

## 6. Inventory Flow (Stock Management)

| Step | Halaman/Action     | Keterangan                        |
| ---- | ------------------ | --------------------------------- |
| 1    | Buka halaman Stok  | List stok per toko                |
| 2    | Mutasi stok        | Stock In / Stock Out / Adjustment |
| 3    | Isi produk & qty   | Required                          |
| 4    | Simpan mutasi      | POST /inventory                   |
| 5    | Catat riwayat stok | Tersimpan sebagai ledger          |

---

## 7. User & Role Management Flow

| Step | Halaman/Action       | Keterangan         |
| ---- | -------------------- | ------------------ |
| 1    | Buka User Management | Hanya Owner/Admin  |
| 2    | Tambah user          | Username, password |
| 3    | Assign role          | owner/admin/kasir  |
| 4    | Assign ke toko       | Jika multi-store   |
| 5    | Simpan               | POST /users        |

---

## 8. Store Management Flow

| Step | Halaman/Action        | Keterangan   |
| ---- | --------------------- | ------------ |
| 1    | Buka Store Management | Hanya Owner  |
| 2    | Tambah store          | Nama, alamat |
| 3    | Simpan                | POST /stores |
| 4    | Assign user ke store  | Opsional     |

---

## 9. Audit Trail Flow

| Step | Halaman/Action      | Keterangan                 |
| ---- | ------------------- | -------------------------- |
| 1    | Aksi terjadi        | CRUD produk/penjualan/stok |
| 2    | Sistem log otomatis | User, modul, aksi          |
| 3    | Buka Audit Trail    | Filter log                 |

**Contoh log**

| Waktu            | User  | Modul   | Aksi   | Detail                |
| ---------------- | ----- | ------- | ------ | --------------------- |
| 2025-10-21 09:30 | admin | PRODUCT | UPDATE | Harga 10.000 → 12.000 |

---

## 10. Logout & Session Flow

| Step | Halaman/Action  | Keterangan                   |
| ---- | --------------- | ---------------------------- |
| 1    | Klik Logout     | Hapus access + refresh token |
| 2    | Redirect        | Kembali ke halaman Login     |
| 3    | Session timeout | Otomatis logout              |

---

Dokumen ini menjadi panduan awal untuk membuat UI Wireframe dan implementasi frontend berdasarkan React.
