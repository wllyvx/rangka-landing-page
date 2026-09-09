# ADR 0001 — Pecah `index.astro` menjadi komponen per-section

Status: diterima
Tanggal: 2026-09-09

## Konteks

`src/pages/index.astro` (786 baris) memuat seluruh landing — Header, Hero, Layanan, Gaya, Proses, SituasiContoh, Kontak, Footer — plus satu `<script>` besar berisi empat perhatian (reveal, spine, nav-menu, template chat). Sulit dinavigasi dan berisiko konflik saat disunting.

## Keputusan

- Pecah per-section ke `src/components/landing/`: `Header`, `Hero`, `Layanan`, `Gaya`, `Proses`, `SituasiContoh`, `Kontak`, `Footer`.
- Komponen bersama minimal: `IkonPanah` (panah 16px yang diulang di Hero + Layanan) dan `SkripReveal` (observer reveal-on-scroll, dipasang sekali dari `index.astro`).
- Isi section tetap hardcode (tanpa lapisan data/props). Refactor murni pemindahan kode.
- Script colocated dengan pemiliknya: nav-menu di `Header`, spine-scroll di `Proses`, salin-template + cakupan di `Kontak`, reveal di `SkripReveal`.
- Penamaan Indonesia PascalCase mengikuti id section; komponen untuk anchor `#umpan-balik` dinamai `SituasiContoh` karena isinya contoh kebutuhan ilustratif, bukan testimoni.
- `index.astro` tinggal komposisi (~30 baris).

## Alternatif yang dipertimbangkan

- Ekstrak data Layanan/Proses ke `src/data/` + props — ditolak untuk ronde ini agar diff murni pemindahan dan mudah direview.
- Satu script global tetap di `index.astro` — ditolak karena logika nav/template/spine milik section masing-masing.
- Pecah SVG ilustrasi ke file sendiri — ditunda; ilustrasi tetap inline di `Hero`/`Gaya`.

## Konsekuensi

- `index.astro` mudah dibaca; perubahan satu section tidak menyentuh file lain.
- Kontrak antar-section lewat DOM tetap ada: link `a[data-layanan]` di `Layanan` dibaca oleh script di `Kontak`; id `spine-wrap`/`spine-fill` milik `Proses`; kelas `.reveal` lintas section diinisialisasi `SkripReveal`. Jangan ganti nama atribut/id/kelas ini tanpa memeriksa pasangan yang memakai.
