# 🧾 TokoFlow Documentation

Selamat datang di dokumentasi resmi **TokoFlow** — platform SaaS untuk sistem kasir dan manajemen stok multi-toko.  
Dokumentasi ini menjadi panduan lengkap bagi **developer**, **QA**, dan **tim implementasi** untuk memahami struktur, fitur, serta alur kerja sistem TokoFlow.

---

## 📘 Struktur Dokumentasi

| File                       | Deskripsi                                                                             |
| -------------------------- | ------------------------------------------------------------------------------------- |
| [overview.md](overview.md) | Ringkasan sistem, tujuan, ruang lingkup, peran pengguna, dan teknologi yang digunakan |
| [features.md](features.md) | Daftar modul & fitur utama, dependensi antar fitur, dan prioritas pengembangan        |
| [ui-flow.md](ui-flow.md)   | Alur navigasi dan interaksi pengguna per modul (UI Flow & Onboarding)                 |
| [erd.md](erd.md)           | Entity Relationship Diagram (ERD) dan struktur database (DBML)                        |
| [api-spec.md](api-spec.md) | Spesifikasi API lengkap dengan contoh request & response                              |
| [use-case.md](use-case.md) | Use case utama berdasarkan peran pengguna (Owner, Admin, Kasir) dan alur SaaS         |

---

## 🎯 Tujuan Dokumentasi

Dokumentasi ini dibuat untuk:

- ✅ Menjadi panduan pengembangan backend & frontend (**Node.js + React**)
- ✅ Menjadi referensi integrasi dan testing **QA**
- ✅ Mendukung onboarding developer baru agar cepat memahami arsitektur sistem
- ✅ Menyediakan gambaran arus kerja **SaaS multi-tenant** (Owner, Admin, Kasir)

---

## 🚀 Panduan Navigasi Cepat

1. **Mulai dari `overview.md`**  
   Untuk memahami konsep SaaS TokoFlow dan tujuan sistem.

2. **Lanjut ke `features.md`**  
   Lihat daftar modul aktif dan rencana pengembangan tahap berikutnya.

3. **Gunakan `ui-flow.md`**  
   Pelajari alur interaksi pengguna termasuk proses onboarding tenant baru.

4. **Pelajari `erd.md`**  
   Pahami struktur database untuk implementasi backend (**Sequelize ORM**).

5. **Implementasikan API dengan `api-spec.md`**  
   Ikuti format endpoint sesuai spesifikasi resmi dan uji melalui **Postman Collection**.

6. **Lihat `use-case.md`**  
   Pahami siapa yang melakukan apa dalam sistem, lengkap dengan flow per peran.
