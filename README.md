<p align="center">
  <img src="https://postimg.cc/TymFFdFV' target='_blank'><img src='https://i.postimg.cc/TymFFdFV/logo-1.png' border='0' alt='logo-1'></a>" width="220">
</p>

<p align="center">
Deploy • Github • Vercel • Deploy To Web
</p>

# Deploy_File_Web

Dashboard satu halaman untuk mengubah berkas ZIP menjadi repositori GitHub atau deployment Vercel — langsung dari browser, tanpa git CLI dan tanpa terminal.

Terinspirasi dari alur kerja **Deploin**, dibangun ulang sebagai single-file HTML dengan identitas visual sendiri (dark neobrutalism, aksen violet–lime–cyan).

---

## ✨ Fitur

- **Dashboard** — ringkasan jumlah repositori GitHub & project Vercel secara realtime
- **Repositori** — lihat, buat, dan hapus repositori GitHub milikmu
- **Project** — lihat seluruh project Vercel yang terhubung dengan token kamu
- **Unggah ZIP**
  - **Ke GitHub** — ekstrak ZIP di browser, lalu push seluruh berkas sebagai **satu commit** (via Git Data API: blob → tree → commit → update ref)
  - **Ke Vercel** — ekstrak ZIP, lalu deploy langsung sebagai production deployment (via Deployments API), dengan log proses realtime
- **Pengaturan** — kelola/putuskan token, ganti tema terang/gelap
- 100% client-side — tidak ada server, tidak ada database

---

## 🔑 Cara Login

Deploy_File_Web 
**tidak memakai popup OAuth "Masuk dengan GitHub"** seperti kebanyakan dashboard, karena OAuth code-exchange butuh *client secret* yang harus disimpan di server — sesuatu yang tidak bisa dilakukan dengan aman di file HTML statis tanpa backend.

Sebagai gantinya, dipakai **Personal Access Token (PAT)** — fungsinya sama persis (bisa baca profil, buat/push/hapus repo, atau deploy ke Vercel), hanya cara masuknya beda.

### Token GitHub
1. Buka [github.com/settings/tokens/new](https://github.com/settings/tokens/new)
2. Beri nama token, atur masa berlaku
3. Centang scope:
   - `repo` (buat, ubah, push ke repositori)
   - `delete_repo` (khusus kalau mau bisa hapus repo dari dashboard)
4. Generate, lalu tempel di halaman **Masuk**

### Token Vercel
1. Buka [vercel.com/account/tokens](https://vercel.com/account/tokens)
2. Buat token baru
3. Tempel di halaman **Masuk**

> Token disimpan **hanya di `localStorage` browser kamu sendiri** dan dikirim langsung ke `api.github.com` / `api.vercel.com`. Tidak ada server perantara yang menyimpan atau melihat token ini.

---

## 🚀 Cara Menjalankan

Karena ini file HTML tunggal (tidak butuh build step), cukup:

1. Buka `Deploy_File_Web.html` langsung di browser, **atau**
2. Host di mana saja yang bisa serve file statis: GitHub Pages, Vercel, Netlify, Cloudflare Pages, dsb.

```bash
# contoh cepat pakai server statis lokal
npx serve .
```

Tidak ada dependensi build, `npm install`, atau environment variable yang perlu diatur — satu-satunya library eksternal (JSZip) dimuat lewat CDN di dalam file.

---

## 🧱 Struktur

Semuanya ada dalam satu file:

```
Deploy_File_Web.html
├── <style>   → seluruh CSS (tema, komponen, layout)
└── <script>  → router hash-based, state management, pemanggilan API,
                logika ekstraksi ZIP (JSZip), dan push/deploy
```

Routing memakai hash (`#/dashboard`, `#/repos`, `#/projects`, `#/upload`, `#/settings`) sehingga tidak butuh konfigurasi server untuk client-side routing.

---

## ⚠️ Keterbatasan yang perlu diketahui

- **Belum diuji end-to-end** dengan token GitHub/Vercel sungguhan pihak developer — disarankan tes dulu dengan repo/project kecil sebelum dipakai untuk data penting.
- **Ukuran ZIP besar** bisa kena limit payload, terutama saat deploy ke Vercel karena seluruh isi file dikirim sebagai base64 dalam satu request `POST /v13/deployments`.
- **Login bukan OAuth resmi** — lihat bagian [Cara Login](#-cara-login) di atas.
- Tidak ada fitur edit/redeploy project Vercel yang sudah ada dari dashboard (baru bisa lihat daftar + deploy baru).

---

## 🔒 Privasi & Keamanan

- Tidak ada backend, tidak ada database, tidak ada analytics pihak ketiga.
- Token PAT hanya hidup di `localStorage` browser — hapus dengan tombol "Putuskan" di halaman Pengaturan, atau bersihkan storage browser secara manual.
- Semua panggilan API langsung dari browser kamu ke `api.github.com` / `api.vercel.com` menggunakan HTTPS.

---

## 📄 Lisensi

Bebas dipakai, dimodifikasi, dan disebarluaskan untuk keperluan pribadi maupun komersial.
# Deploy_File_Web
