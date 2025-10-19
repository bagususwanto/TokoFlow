# 📚 Dokumentasi Sistem Kasir & Stok Toko Kecil

Selamat datang di direktori dokumentasi proyek **Sistem Kasir & Stok Toko Kecil**.  
Folder ini berisi seluruh panduan teknis, desain sistem, dan petunjuk implementasi proyek — ditulis dengan format **Markdown (.md)** agar mudah dibaca, diubah, dan diintegrasikan dengan GitHub Pages atau Docs-as-Code.

---

## 📁 Struktur Dokumentasi

/docs
┣ overview.md ← Deskripsi umum dan tujuan proyek
┣ features.md ← Fitur utama sistem
┣ tech-stack.md ← Teknologi yang digunakan
┣ architecture.md ← Arsitektur sistem (backend–frontend–database)
┣ database-schema.md ← Struktur database (DBML format)
┣ api-spec.md ← Spesifikasi endpoint API
┣ ui-wireframe.md ← Rancangan tampilan antarmuka (UI)
┣ user-flow.md ← Alur penggunaan sistem
┣ installation.md ← Panduan instalasi & setup
┣ usage.md ← Panduan penggunaan sistem
┣ deployment.md ← Panduan deploy ke server/Render
┣ maintenance.md ← Panduan perawatan & troubleshooting
┗ readme.md ← Berkas ini (pengantar dokumentasi)

---

## 🧭 Panduan Navigasi

| File                 | Isi Singkat                                         | Tujuan                                                   |
| -------------------- | --------------------------------------------------- | -------------------------------------------------------- |
| `overview.md`        | Ringkasan proyek, latar belakang, dan tujuan sistem | Memberi konteks umum sebelum membaca dokumen lain        |
| `features.md`        | Daftar fitur utama dan fungsi masing-masing         | Memahami ruang lingkup proyek                            |
| `tech-stack.md`      | Daftar teknologi yang digunakan (FE, BE, DB, Tools) | Mengetahui komponen utama sistem                         |
| `architecture.md`    | Diagram & penjelasan arsitektur sistem              | Menunjukkan bagaimana komponen saling terhubung          |
| `database-schema.md` | Definisi tabel database dengan format **DBML**      | Panduan implementasi atau migrasi database               |
| `api-spec.md`        | Daftar endpoint API dan response format             | Referensi untuk frontend & integrasi eksternal           |
| `ui-wireframe.md`    | Sketsa UI (gambar atau deskripsi)                   | Dasar desain frontend                                    |
| `user-flow.md`       | Diagram atau penjelasan alur pengguna               | Memahami perjalanan pengguna dari login sampai transaksi |
| `installation.md`    | Langkah-langkah instalasi & konfigurasi proyek      | Setup awal di lokal developer                            |
| `usage.md`           | Cara menggunakan sistem (frontend & backend)        | Panduan pengguna internal                                |
| `deployment.md`      | Panduan deploy ke server (Render / Nginx / PM2)     | Menjalankan sistem di lingkungan produksi                |
| `maintenance.md`     | Panduan perawatan, backup, dan update               | Dokumentasi teknis pasca-deploy                          |

---

## 🧩 Format & Standar Penulisan

- Gunakan format Markdown (`.md`) untuk seluruh dokumen.
- Hindari tabel yang terlalu kompleks untuk memudahkan edit langsung.
- Gunakan komentar `//` atau catatan `[note: ...]` untuk memberikan keterangan tambahan.
- Nama file **huruf kecil semua** dan **dipisahkan tanda hubung (-)**.

---

## 🛠️ Tools Dokumentasi

Dokumentasi ini ditulis agar kompatibel dengan:

- [**dbdiagram.io**](https://dbdiagram.io) — untuk file `database-schema.md`
- [**draw.io / diagrams.net**](https://app.diagrams.net/) — untuk `ui-wireframe.md` & `user-flow.md`
- [**Markdown Preview Enhanced (VS Code)**](https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced) — untuk melihat hasil Markdown dengan diagram

---

## 📜 Lisensi

Seluruh dokumentasi mengikuti lisensi proyek utama:  
**MIT License © 2025**  
Gunakan sesuai ketentuan lisensi pada file [`/LICENSE`](../LICENSE).

---

## 👥 Kontribusi Dokumentasi

Jika kamu menambah atau memperbarui dokumentasi:

1. Gunakan format dan gaya penulisan yang konsisten.
2. Simpan gambar atau diagram ke `/docs/assets` (jika ada).
3. Tambahkan tautan antar dokumen agar navigasi mudah.
4. Lakukan commit dengan pesan jelas, contoh:
   ```bash
   git commit -m "docs: update api-spec.md with new endpoints"
   ```
