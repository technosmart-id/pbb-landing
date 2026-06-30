# SIM-PBB SMART! — Landing Page

Landing page statis untuk **SIM-PBB SMART!** — Sistem Informasi Manajemen PBB-P2
yang cerdas, akurat, dan terpetakan. Dirancang untuk Bapenda modern.

Dibangun sebagai **satu file HTML statis** dengan Tailwind (Play CDN) — tanpa
build step, tanpa framework. Cukup push ke GitHub dan langsung ter-deploy ke
GitHub Pages.

## ✨ Highlight

- **Satu file** — semua ada di [`index.html`](./index.html). Tidak ada dependency, tidak ada `npm install`.
- **Tailwind via Play CDN** — utility classes penuh dengan tema kustom (cadastral palette) yang dikonfigurasi inline.
- **Light mode default + dark mode mengikuti OS** — beralih otomatis via `prefers-color-scheme`, tanpa toggle, tanpa flicker.
- **Aesthetic "Cadastral Survey"** — tekstur peta bidang, garis kontur, tick koordinat, north arrow, dan scale bar. Tipografi: Fraunces (display) + Plus Jakarta Sans (body) + JetBrains Mono (label teknis).
- **Ikon SVG inline** (sprite `<symbol>`) — ringan, tajam, tanpa library tambahan.
- **Aksesibilitas** — `prefers-reduced-motion` dihormati, struktur semantik, kontras AA.

## 🚀 Deploy ke GitHub Pages

Repo ini sudah punya workflow [`deploy.yml`](./.github/workflows/deploy.yml) yang
otomatis memublikasikan situs setiap push ke `main`.

**Aktifkan sekali saja:**

1. Buka **Settings → Pages** repo di GitHub.
2. Pada **Source**, pilih **GitHub Actions**.
3. Push commit apa pun ke `main` (atau jalankan workflow manual via tab **Actions**).

Situs akan tersedia di:

```
https://<organisasi-atau-user>.github.io/<nama-repo>/
```

> Alternatif tanpa workflow: di **Settings → Pages** pilih
> **Deploy from a branch** → `main` / `root`. Karena ini HTML murni, cara itu juga langsung jalan.

## 🧑‍💻 Menjalankan secara lokal

Tidak perlu build. Cukup buka `index.html` di browser, atau serve dengan static server:

```bash
# opsi 1: Python
python -m http.server 5173

# opsi 2: Node (jika punya npx)
npx serve .
```

Lalu buka `http://localhost:5173`.

## 🎨 Kustomisasi singkat

| Ingin mengubah… | Lokasi |
| --- | --- |
| Warna tema (light/dark) | token `--c-*` di dalam `<style>` (`:root` & `@media prefers-color-scheme`) |
| Tema Tailwind (font/warna) | objek `tailwind.config` di `<head>` |
| Copy / teks | langsung di markup HTML masing-masing `<section>` |
| Font | `<link>` Google Fonts + `fontFamily` di config |

## 📝 Catatan produksi

Play CDN memproses Tailwind di browser (JIT) — ideal untuk situs statis tanpa build,
namun menghasilkan warning di console. Untuk performa puncak (CSS terkompilasi,
tanpa request CDN), bisa dikompilasi sekali dengan Tailwind CLI:

```bash
npx tailwindcss -i ./src/input.css -o ./styles.css --minify
```

…lalu ganti tag `<script src="https://cdn.tailwindcss.com">` dengan
`<link rel="stylesheet" href="./styles.css">`. Untuk kebutuhan landing page saat ini,
versi CDN sudah lebih dari cukup.

---

© SIM-PBB SMART! · Tata kelola Pajak Daerah & PBB-P2.
