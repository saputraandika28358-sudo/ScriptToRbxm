# ScriptToRbxm# ScriptToRbxm

Konverter dua arah antara file Roblox Model/Place (`.rbxm`, `.rbxmx`, `.rbxl`, `.rbxlx`) dan Lua script — plus bisa langsung publish hasilnya ke Roblox jadi Model/Asset ID. Semuanya jalan **100% di browser**, tanpa server backend, tanpa data yang diupload ke pihak lain selain langsung ke Roblox saat kamu klik Publish.

Dibuat oleh **Kloz — zir_live**.
Credits konsep parsing: [fiveman1/rbxm-parser-ts](https://github.com/fiveman1/rbxm-parser-ts)

---

## ✨ Fitur

**🔄 Convert (RBXM/RBXL → Script)**
- Upload `.rbxm`, `.rbxmx`, `.rbxl`, atau `.rbxlx`
- Parser XML (`.rbxmx`/`.rbxlx`) full-support, parser binary (`.rbxm`/`.rbxl`) best-effort/beta
- Explorer tree + filter per class, panel Properties, Script Viewer dengan syntax highlighting Lua + nomor baris
- Export satu script (`.lua`) atau semua script sekaligus (`.zip`)
- Export struktur instance ke `.json`

**🛠️ Build (Script → RBXM)**
- Tambah banyak Script/LocalScript/ModuleScript (ketik langsung atau upload `.lua`, bisa banyak sekaligus)
- Atur "taruh di mana" (lokasi service tujuan) per script
- Generate sebagai `.rbxm` (binary asli) atau `.rbxmx` (XML)
- Preview isi file sebelum download
- Edit-in-place: klik kartu script buat ubah lagi

**🚀 Publish**
- Upload atau kirim langsung file hasil Convert/Build ke Roblox lewat **Open Cloud API**
- Isi Nama Asset, Deskripsi, Publish sebagai User/Group, API Key
- Dapat Model/Asset ID langsung setelah proses moderasi Roblox selesai
- Riwayat publish tersimpan lokal di browser

**🕑 History & ⚙️ Settings**
- Riwayat file yang pernah diproses (lokal, browser-only)
- Ganti tema Light/Dark (glassmorphism)

---

## 🚀 Cara Deploy

1. Ekstrak seluruh isi paket ini (jangan pisahkan `index.html` dari folder `assets/`).
2. Upload semua file ke hosting statis, misalnya:
   - **GitHub Pages**: push ke repo, aktifkan Pages dari branch/folder yang berisi file-file ini.
   - **Netlify / Vercel / Cloudflare Pages**: drag-and-drop folder ini ke dashboard mereka.
3. Buka URL hasil deploy — website langsung jalan, tidak perlu build step apapun.

### Struktur file
```
index.html          ← halaman utama (semua logic ada di sini)
robots.txt
sitemap.xml
site.webmanifest
assets/
  favicon.ico, favicon-16x16.png, favicon-32x32.png, favicon-48x48.png
  apple-touch-icon.png, icon-192.png, icon-512.png, logo.png
  og-image.png
```

## 🔑 Setup Publish ke Roblox (Open Cloud API)

1. Login ke [create.roblox.com/dashboard/credentials](https://create.roblox.com/dashboard/credentials).
2. Klik **Create API Key**, kasih nama bebas.
3. Di **Select API System**, pilih `assets`, centang **Read** dan **Write**.
4. Simpan, copy API key-nya (cuma muncul sekali).
5. Tempel di tab **Publish** pada website, lengkap dengan User ID / Group ID kamu.

Tutorial lengkap dengan langkah bergambar juga ada langsung di dalam tab Publish website (klik "Cara pakai").

## ⚠️ Keterbatasan yang perlu diketahui

- **Parser binary** (`.rbxm`/`.rbxl`) ditulis berdasarkan spesifikasi publik format Roblox tanpa akses ke Roblox Studio asli untuk pengetesan langsung — sebagian tipe properti langka mungkin belum akurat 100%. Kalau ragu, gunakan format XML (`.rbxmx`/`.rbxlx`) yang jauh lebih teruji.
- **Penulisan `.rbxm` (Build → Publish)** sudah divalidasi lewat roundtrip encode-decode internal (semua data balik cocok), tapi belum divalidasi langsung terhadap Roblox Studio asli. Kalau file ditolak Studio, coba format `.rbxmx` sebagai alternatif.
- **Publish API** memanggil `apis.roblox.com` langsung dari browser. Kalau ada masalah koneksi/CORS, error akan ditampilkan di layar — laporkan pesannya kalau butuh perbaikan.
- API Key hanya disimpan di `localStorage` browser kamu sendiri **jika kamu aktifkan** opsi "Ingat API key" — tidak pernah dikirim ke server manapun selain langsung ke Roblox.

## 🔒 Privasi

Semua parsing, generate file, dan penyimpanan riwayat berjalan lokal di browser (client-side). Satu-satunya request keluar adalah saat kamu menekan tombol **Publish**, yang mengirim file dan API key langsung ke `apis.roblox.com` — tidak pernah lewat server pihak ketiga.
