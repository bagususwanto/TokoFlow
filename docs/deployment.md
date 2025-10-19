# 🚀 Panduan Deploy ke Render

Panduan ini menjelaskan langkah-langkah melakukan deployment **Sistem Kasir & Stok Toko Kecil** ke platform **Render** menggunakan konfigurasi standar.

---

## 1. Persiapan

Pastikan:

- Repositori sudah di-push ke GitHub/GitLab.
- Folder `backend/` dan `frontend/` sudah berisi file `package.json`.
- `.env` sudah dikonfigurasi (tanpa data sensitif dikomit).

---

## 2. Deploy Backend

1. Buka [https://render.com](https://render.com)
2. Klik **New → Web Service**
3. Hubungkan ke repository kamu.
4. Pilih:
   - **Branch:** `main`
   - **Root directory:** `backend/`
   - **Build Command:**
     ```
     npm install
     ```
   - **Start Command:**
     ```
     npm run start
     ```
5. Tambahkan Environment Variables sesuai `.env` backend.
6. Klik **Create Web Service**.

---

## 3. Deploy Frontend

1. Klik **New → Static Site**
2. Pilih repository yang sama.
3. Atur:
   - **Root directory:** `frontend/`
   - **Build Command:**
     ```
     npm install && npm run build
     ```
   - **Publish Directory:**
     ```
     dist
     ```
4. Tambahkan Environment Variable:

```bash
VITE_API_URL=https://<backend-service-name>.onrender.com
```

5. Klik **Create Static Site**.

---

## 4. Uji Koneksi

Setelah kedua service aktif:

- Buka URL frontend Render.
- Coba login dan transaksi.
- Pastikan data tersimpan dengan benar.

---

## 5. Tips & Best Practice

✅ Gunakan **Render Cron Jobs** untuk backup database otomatis.  
✅ Aktifkan **Auto Deploy** agar setiap push ke `main` langsung update.  
✅ Simpan `.env` hanya di dashboard Render (jangan dikomit ke GitHub).  
✅ Gunakan domain custom dengan SSL gratis dari Render.

---

## ✅ Deployment Selesai

Sistem kini aktif di cloud, siap digunakan untuk operasional toko.
