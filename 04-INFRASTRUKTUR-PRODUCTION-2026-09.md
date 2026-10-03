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

## 2. Daftar Agen Produksi

Seluruh agen berikut terpantau berjalan pada pemeriksaan 3 Oktober 2026:

| Agen | Peran | Status |
|---|---|---|
| Aplikasi web | Situs publik, katalog produk, pendaftaran, dan portal kelas siswa | Beroperasi |
| API utama | Transaksi penjualan, data produk, penilaian, dan pelaporan | Beroperasi |
| API pendamping | Layanan data pendukung operasional | Beroperasi |
| Gerbang pesan | Komunikasi waktu nyata dan pengiriman pesan WhatsApp (notifikasi, tindak lanjut) | Beroperasi |
| Pekerja AI | Antrean tugas kecerdasan buatan (rekomendasi, penilaian, penerbitan) | Beroperasi |
| Agen suara Tutor AI | Percakapan suara dan obrolan Tutor AI dalam satu sesi | Beroperasi |
| Agen kelas | Pendamping pembelajaran di ruang kelas digital | Beroperasi |
| Pengawas kelas | Pengawasan kualitas sesi kelas digital | Beroperasi |
| Penerbit konten | Penerbitan artikel dan materi pemasaran organik terjadwal | Beroperasi |
| Penjaga forum | Moderasi forum diskusi | Beroperasi |
| Pemeriksa media forum | Pemeriksaan kualitas media pada forum | Beroperasi |
| Bot diskusi | Layanan percakapan pendukung komunitas belajar | Beroperasi |
| Layanan pencarian | Pencarian materi berbasis basis pengetahuan internal | Beroperasi |
| Pengendali operasional | Pengaturan tugas operasional terjadwal | Beroperasi |
| Basis data | Penyimpanan seluruh data transaksi dan operasional (akses internal saja) | Beroperasi |
| Tembolok | Tembolok dan antrean (akses internal saja) | Beroperasi |
| Penyimpanan media | Penyimpanan berkas statis dan media melalui jaringan distribusi konten | Beroperasi |

Setiap agen dipantau dan dipulihkan otomatis apabila berhenti.

---

## 3. Keputusan Ruang Lingkup

| Keputusan | Status | Dasar |
|---|---|---|
| Layanan pembuatan gambar (SD WebUI) | Di luar lingkup — tidak digunakan dan tidak berjalan di produksi | Verifikasi produksi 3 Oktober 2026 |
| Segmen Sidang, Interview, dan Karier | Ditangguhkan — seluruh halaman dan produk terkait dinonaktifkan | Arahan pemegang saham, 20 September 2026 |
| Subdomain aplikasi (`app.*`) | Menunggu keputusan — diarahkan ke layanan utama atau dihentikan | Menunggu keputusan manajemen |
| Akses pemantauan internal | Di luar lingkup dokumen ini — dikelola terpisah secara internal | Kebijakan keamanan informasi |
| Aplikasi seluler native | Tidak dibangun — situs web dan pesan instan dinilai mencukupi | Model bisnis 2026–2028 |

---

## 4. Alur Permintaan

Permintaan publik diterima melalui penyeimbang lalu lintas (Nginx) dan diteruskan sesuai jenisnya:

- Halaman web → aplikasi web produksi
- Transaksi dan data (`/api/`) → API utama dan API pendamping
- Pesan waktu nyata dan WhatsApp → gerbang pesan
- Layanan suara Tutor AI → agen suara
- Berkas media → jaringan distribusi konten

Seluruh layanan internal hanya dapat diakses dari dalam server dan tidak terbuka ke publik.

---

## 5. Operasional

- Seluruh agen dikelola oleh pengelola proses (PM2) dengan pemulihan otomatis apabila berhenti.
- Kesehatan layanan dipantau berkala (situs, API, gerbang pesan, agen suara).
- Titik pemulihan rilis sebelumnya tersedia di server produksi untuk kebutuhan pengembalian darurat.
- Prosedur rilis berikutnya yang disarankan: hentikan seluruh layanan sementara saat pembangunan versi produksi, jalankan pembangunan, verifikasi, lalu pulihkan layanan.

---

## 6. Tindak Lanjut

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
