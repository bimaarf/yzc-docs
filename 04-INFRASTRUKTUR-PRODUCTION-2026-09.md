# Infrastruktur Produksi Yz-Course (per 3 Oktober 2026)

- **Status:** Terverifikasi melalui pemeriksaan langsung layanan produksi pada 3 Oktober 2026. Beberapa item ditandai untuk tindak lanjut.
- **Sumber:** Pemeriksaan langsung layanan produksi, berkas konfigurasi repositori sistem, dan pemeriksaan respons situs publik.
- **Klasifikasi:** Internal — dokumen ini tidak memuat kredensial, alamat server, maupun akses operasional.

---

## 1. Layanan Publik

| Layanan | Kondisi |
|---|---|
| Situs utama (`yz-course.com`) | Beroperasi normal (respons 200) — melayani aplikasi web produksi |
| Subdomain aplikasi (`app.*`) | Belum beroperasi (respons 502) — menunggu keputusan manajemen |

---

## 2. Produk dan Agen yang Beroperasi

Seluruh layanan berikut terpantau berjalan pada pemeriksaan 3 Oktober 2026:

| Layanan | Fungsi Bisnis |
|---|---|
| Aplikasi web (Next.js) | Situs publik, katalog produk, pendaftaran, dan portal kelas siswa |
| API utama (Laravel) | Transaksi penjualan, data produk, penilaian, dan pelaporan |
| API pendamping | Layanan data pendukung operasional |
| Gerbang pesan (Socket-WA) | Komunikasi waktu nyata dan pengiriman pesan WhatsApp (notifikasi, tindak lanjut) |
| Pekerja AI | Antrean tugas kecerdasan buatan (rekomendasi, penilaian, penerbitan) |
| Agen suara Tutor AI | Percakapan suara dan obrolan Tutor AI dalam satu sesi |
| Agen kelas (Classroom AI) | Pendamping pembelajaran di ruang kelas digital beserta pengawas kualitas sesi |
| Penerbit konten | Penerbitan artikel dan materi pemasaran organik terjadwal |
| Penjaga forum | Moderasi forum diskusi dan pemeriksaan kualitas media |
| Bot diskusi | Layanan percakapan pendukung komunitas belajar |
| Layanan pencarian (RAG) | Pencarian materi berbasis basis pengetahuan internal |
| Pengendali operasional | Orkestrasi tugas operasional terjadwal |
| Basis data (PostgreSQL) | Penyimpanan seluruh data transaksi dan operasional (akses internal saja) |
| Tembolok (Redis) | Tembolok dan antrean (akses internal saja) |
| Penyimpanan media | Penyimpanan objek dan jaringan distribusi konten untuk berkas statis dan media |

**Klarifikasi:** layanan pembuatan gambar (SD WebUI) **tidak digunakan** dan tidak berjalan di lingkungan produksi. Seluruh rujukan sebelumnya terhadap layanan tersebut dinyatakan tidak berlaku.

---

## 3. Alur Permintaan

Permintaan publik diterima melalui penyeimbang lalu lintas (Nginx) dan diteruskan sesuai jenisnya:

- Halaman web → aplikasi web produksi
- Transaksi dan data (`/api/`) → API utama dan API pendamping
- Pesan waktu nyata dan WhatsApp → gerbang pesan
- Layanan suara Tutor AI → agen suara
- Berkas media → jaringan distribusi konten

Seluruh layanan internal hanya dapat diakses dari dalam server dan tidak terbuka ke publik.

---

## 4. Operasional

- Seluruh agen dikelola oleh pengelola proses (PM2) dengan pemulihan otomatis apabila berhenti.
- Kesehatan layanan dipantau berkala (situs, API, gerbang pesan, agen suara).
- Titik pemulihan rilis sebelumnya tersedia di server produksi untuk kebutuhan pengembalian darurat.
- Prosedur rilis berikutnya yang disarankan: hentikan seluruh layanan sementara saat pembangunan versi produksi, jalankan pembangunan, verifikasi, lalu pulihkan layanan.

---

## 5. Tindak Lanjut

| # | Item | Penanggung Jawab | Prioritas |
|---|---|---|---|
| 1 | Keputusan atas subdomain aplikasi (`app.*`): arahkan ke layanan utama atau hentikan | Manajemen | Sedang |
| 2 | Sinkronisasi berkas konfigurasi lalu lintas di repositori dengan konfigurasi aktual server | Teknis | Sedang |
| 3 | Validasi tagihan server dan penyimpanan media untuk rekonsiliasi angka operasional | Keuangan | Sedang |

---

## Keputusan yang Dibutuhkan

1. Persetujuan atas penghapusan seluruh rujukan layanan pembuatan gambar dari dokumen perusahaan lainnya.
2. Keputusan atas nasib subdomain aplikasi (`app.*`).

## Langkah Selanjutnya

1. Tim teknis menutup rujukan layanan yang tidak digunakan pada dokumen terkait.
2. Manajemen menetapkan keputusan subdomain aplikasi sebelum kampanye berikutnya.
3. Tim keuangan memvalidasi tagihan infrastruktur terhadap rencana anggaran.
