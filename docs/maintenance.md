# 🧰 Panduan Maintenance

Dokumen ini menjelaskan cara menjaga, memantau, dan memperbarui sistem agar tetap stabil dan aman.

---

## 🔄 1. Backup Database

### Manual

Jalankan perintah di server:

```bash
pg_dump -U postgres store-pos > backup_store-pos_db$(date +%Y%m%d).sql
```

### Otomatis (Render Cron Job)

Buat cron job harian:

```bash
pg_dump -U postgres store-pos_db > /data/backup/backup.sql
```

---

## 🧹 2. Update Sistem

### Update Dependensi

```bash
cd backend && npm update
cd ../frontend && npm update
```

### Pull Pembaruan Terbaru

```bash
git pull origin main
```

---

## ⚙️ 3. Monitoring

- Gunakan **Render Dashboard** untuk melihat log backend.
- Aktifkan **Health Check** pada service backend.
- Cek log lokal:

```bash
tail -f logs/app.log
```

---

## 🧑‍💻 4. User Management

- Hapus akun kasir yang sudah tidak aktif.
- Gunakan password kuat dan ubah secara berkala.
- Batasi akses admin hanya untuk pemilik atau manajer toko.

---

## 🔐 5. Keamanan

- Jangan commit file `.env` ke GitHub.
- Ganti `JWT_SECRET` minimal setiap 6 bulan.
- Batasi CORS hanya untuk domain frontend resmi.

---

## 🧾 6. Maintenance Rutin (Checklist)

| Aktivitas         | Frekuensi | Penanggung Jawab |
| ----------------- | --------- | ---------------- |
| Backup database   | Harian    | Admin            |
| Update dependensi | Bulanan   | Developer        |
| Audit user aktif  | Mingguan  | Pemilik          |
| Cek error log     | Harian    | Admin            |

---

## ✅ Selesai

Dengan perawatan rutin, sistem akan tetap aman, stabil, dan optimal untuk digunakan dalam jangka panjang.
