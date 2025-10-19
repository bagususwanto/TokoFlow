# 💻 Panduan Penggunaan Sistem Kasir & Stok Toko Kecil

Panduan ini menjelaskan cara menggunakan aplikasi setelah berhasil dijalankan secara lokal atau di server.

---

## 🧾 1. Login

1. Buka aplikasi di browser, misalnya:  
   `http://localhost:5173` atau URL deploy kamu.
2. Masukkan:
   - **Username:** admin
   - **Password:** admin123 (atau sesuai konfigurasi awal)
3. Klik **Login**.

---

## 🛍️ 2. Modul Kasir

### Membuat Transaksi Baru

1. Buka menu **Kasir / Penjualan**.
2. Pilih produk yang dibeli.
3. Masukkan jumlah barang.
4. Klik **Proses Pembayaran**.
5. Sistem akan mengurangi stok otomatis.

### Cetak Struk

Setelah transaksi berhasil, klik **Cetak Struk** untuk mencetak atau menyimpan struk dalam format PDF.

---

## 📦 3. Modul Stok Barang

### Tambah Barang Baru

1. Masuk ke menu **Stok Barang**.
2. Klik tombol **Tambah Barang**.
3. Isi form dengan:
   - Nama Barang
   - Kode SKU
   - Harga Beli & Jual
   - Stok Awal
4. Klik **Simpan**.

### Update Stok

1. Pilih barang dari daftar.
2. Klik **Edit**.
3. Ubah jumlah stok, kemudian **Simpan**.

---

## 👥 4. Manajemen Pengguna

1. Masuk ke menu **Pengguna / User Management**.
2. Klik **Tambah Pengguna** untuk menambah akun kasir, admin, atau manajer.
3. Role pengguna menentukan akses menu:
   - **Admin** → Semua fitur
   - **Kasir** → Transaksi & cetak struk
   - **Manajer** → Laporan & stok

---

## 📊 5. Laporan

1. Masuk ke menu **Laporan Penjualan**.
2. Pilih rentang tanggal.
3. Klik **Tampilkan** untuk melihat data transaksi.
4. Klik **Ekspor ke Excel** untuk mengunduh hasil laporan.

---

## 🔒 6. Logout

Klik avatar profil di pojok kanan atas → pilih **Logout**.

---

## ✅ Selesai

Aplikasi siap digunakan untuk mencatat penjualan, mengelola stok, dan memantau kinerja toko harian secara efisien.
