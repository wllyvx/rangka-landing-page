# CONTEXT.md — Rangka Landing Page

Glosarium kanonis. Bukan spec, bukan catatan implementasi.

## Istilah

- **Rangka**: studio interior fiktif untuk hunian (rumah dan apartemen). Selalu ditegaskan sebagai contoh portofolio, bukan biro nyata.
- **Layanan**: empat penawaran tetap — Desain konsep hunian, Gambar kerja + pendampingan, Penataan ulang tanpa bongkar, Kurasi material & furnitur.
- **Gaya**: galeri suasana ruang dalam bentuk ilustrasi SVG (ruang tamu, material, kamar, dapur, catatan denah). Bukan foto proyek nyata.
- **Proses**: tiga tahap tetap — Konsultasi awal, Konsep + gambar kerja, Instalasi + serah terima.
- **SituasiContoh**: tiga kartu contoh kebutuhan ilustratif (apartemen, rumah, kamar tidur). BUKAN testimoni, BUKAN ulasan klien nyata. Istilah lama `umpan-balik` (id anchor `#umpan-balik`) dipertahankan di markup hanya sebagai anchor, nama komponennya `SituasiContoh`.
- **Kontak**: bagian ajakan konsultasi berisi pemilih kebutuhan dan template chat yang bisa disalin.
- **Cakupan**: satu kebutuhan yang dipilih pengguna di Kontak (sama nilainya dengan satu Layanan). Pilihan ini hanya mengisi Template Chat, tidak mengirim apa pun.
- **Template Chat**: teks contoh yang menyesuaikan dengan Cakupan, disalin manual ke aplikasi chat. Tersimpan sementara di `sessionStorage` (`rangka-cakupan`).
