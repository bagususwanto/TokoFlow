# UI & User Flow - Sistem Kasir & Stok Multi-Toko

## Halaman Utama (Wireframe Overview)

Berikut adalah daftar halaman utama dalam sistem berdasarkan rancangan wireframe dan fungsi utama setiap halaman:

| Page                 | Deskripsi                                     |
| -------------------- | --------------------------------------------- |
| **Login**            | Masuk sistem menggunakan username & password  |
| **Dashboard**        | Ringkasan penjualan + notifikasi stok menipis |
| **Kasir (POS)**      | Input transaksi + cetak struk                 |
| **Barang**           | CRUD barang + manajemen stok + riwayat stok   |
| **Kategori Barang**  | Kelola kategori barang                        |
| **Laporan**          | Laporan penjualan + grafik + export Excel     |
| **User Management**  | Kelola user, role, dan akses per toko         |
| **Store Management** | Kelola data toko (multi-store)                |
| **Tools**            | Backup & restore data                         |
| **Activity Logs**    | Audit log aktivitas sistem                    |
| **Profile**          | Ganti password & logout                       |

---

## Alur Pengguna (User Flow)

### 🔐 Autentikasi

```
Login → Input username/password → Validasi JWT → Masuk Dashboard
```

### 🏪 Pemilihan Toko (Multi-Toko)

```
Owner/Admin → Switch toko via dropdown → Reload data berdasarkan toko aktif
```

### 💰 Proses Penjualan (Kasir)

```
Dashboard → Kasir → Pilih toko → Scan/Search barang → Input qty
→ Pilih metode pembayaran (Cash/QRIS/Transfer) → Simpan → Cetak struk
```

### 📦 Manajemen Barang

```
Barang → Tambah/Ubah/Hapus barang → Simpan
→ Update tabel stok + stock_history + activity_log
```

### 🗂️ Manajemen Kategori Barang

```
Kategori Barang → Tambah/Ubah/Hapus kategori → Simpan
```

### 🔧 Update Stok (Stock Adjustment)

```
Barang → Penyesuaian stok → Input qty + alasan → Simpan
→ Dicatat di stock_history & activity_log
```

### 📊 Laporan

```
Laporan Penjualan → Filter (tanggal/toko/kasir) → Export Excel
```

### 🛡️ Activity Logs

```
Activity Logs → Monitoring semua aktivitas user
```

### 💾 Backup & Restore Data

```
Tools → Backup data (export) / Restore data (import) → Simpan ke backup_log
```

### 👤 Profile

```
Profile → Ganti password → Logout
```
