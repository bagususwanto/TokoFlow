# Features - Sistem Kasir & Stok Multi-Toko

## Manajemen Barang

- CRUD barang (tambah, ubah, hapus)
- Kategori barang dinamis
- Barcode unik untuk scan
- Harga & stok per toko
- Minimal stok & notifikasi stok menipis
- Riwayat stok (stock history):

  - **IN** (barang masuk)
  - **OUT** (barang keluar/terjual)
  - **ADJUST** (penyesuaian stok)

## Transaksi Penjualan (Kasir)

- Pilih toko sebelum transaksi
- Input barang via **scan barcode** atau **pencarian cepat**
- Keranjang transaksi: ubah jumlah (qty), hapus item
- Hitung otomatis total + kembalian
- Metode pembayaran: **Cash / QRIS / Transfer**
- Auto-generate nomor invoice
- Cetak struk (**PDF / Thermal Printer**)

## Multi-Toko (Multi-Store)

- Data barang & stok terpisah per toko
- Transaksi dicatat per toko
- Role akses per toko:

  - **Owner** = akses semua
  - **Admin** = toko tertentu
  - **Kasir** = toko tertentu

## Laporan

- Laporan penjualan harian, mingguan, bulanan
- Filter laporan berdasarkan toko, kasir, tanggal
- Top produk terlaris
- Grafik performa penjualan
- Export laporan ke **Excel (.xlsx)**

## Manajemen Pengguna & Role

- Role-based access control (**RBAC**)
- Assign user ke toko tertentu
- Status user: **active / inactive**
- Login aman menggunakan **JWT Authentication**

## Manajemen Toko

- Tambah, ubah, hapus data toko
- Informasi toko: nama, alamat, nomor telepon

## Backup & Restore

- Export/import data (barang, stok, transaksi)
- Backup manual atau otomatis

## Activity Logs (Audit Trail)

- Catat aktivitas penting:

  - login/logout
  - transaksi kasir
  - update stok
  - penghapusan data

- Log detail: user, aksi, toko, waktu, deskripsi
