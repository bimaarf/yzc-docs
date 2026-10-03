# 00 — Standar Dokumen Yz-Course

- **Berlaku untuk:** seluruh dokumen di `Yz-Course-Business-Docs/` yang diberikan kepada investor dan tim.
- **Tanggal berlaku:** 3 Oktober 2026
- **Status:** Mengikat untuk seluruh pembaruan dokumen berikutnya.

---

## 1. Bahasa

1. Seluruh dokumen ditulis dalam **Bahasa Indonesia formal bisnis**.
2. Istilah asing hanya digunakan untuk istilah teknis yang tidak memiliki padanan baku (contoh: CAPEX, OPEX, BEP, CAC, LTV). Setiap istilah didefinisikan satu kali pada kemunculan pertama.
3. Sapaan netral dan konsisten. Tidak menggunakan singkatan percakapan, bahasa kasual, atau campur kode yang tidak perlu.
4. Setiap dokumen ditutup dengan dua bagian: **Keputusan yang dibutuhkan** dan **Langkah selanjutnya**. Tidak ada rekomendasi yang menggantung tanpa pemilik dan tenggat.

## 2. Perlindungan Informasi (Tanpa Kebocoran Prompt)

1. Dokumen final tidak memuat prompt sistem, instruksi internal, atau jejak proses penyusunan (termasuk nama agen, identifikasi sesi, dan catatan orkestrasi).
2. Dokumen final tidak memuat kredensial, alamat IP server, token akses, kunci API, maupun jalur penyimpanan rahasia.
3. Rujukan teknis hanya menunjuk pada lokasi produksi (`yz-course.com`), nama layanan, atau nama berkas konfigurasi yang sudah dipublikasikan — tanpa nilai rahasia.
4. Pemeriksaan akhir setiap dokumen mencakup pemindaian kebocoran informasi sebelum diserahkan kepada investor atau tim.

## 3. Konvensi Angka dan Klaim

1. Setiap angka diberi label: `[F]` fakta bersumber, `[A]` asumsi yang perlu divalidasi, `[?]` belum ditemukan.
2. Setiap asumsi biaya disertai basis perhitungan yang eksplisit.
3. Belanja modal (CAPEX) dan belanja operasional (OPEX) dipisahkan apabila relevan.
4. Setiap rincian anggaran memastikan subtotal dan total konsisten dan dapat ditelusuri ulang.
5. Klaim teknis diverifikasi dari sumber kode `Yz-Course-V2` atau dari pemeriksaan langsung layanan produksi. Klaim dari sumber eksternal mencantumkan sumber dan tanggal akses.
6. Fitur yang tidak ditemukan di kode sumber dinyatakan sebagai belum ditemukan. Tidak ada fitur yang dikarang.

## 4. Struktur Dokumen

1. Dokumen untuk investor (Business Plan, Financial Plan, RAB, Analisis Risiko, Roadmap) mengutamakan narasi hasil, angka yang berlabel, dan keputusan yang diminta.
2. Dokumen untuk tim (Arsitektur Teknis, Infrastruktur & Skalabilitas, Rencana Operasional, Rencana Implementasi) mengutamakan instruksi eksekusi: lokasi berkas atau layanan yang konkret, kriteria sukses yang terukur, pemilik, dan tenggat.
3. Dokumen historis yang tidak lagi berlaku dipindahkan ke `arsip/` dan tidak dihapus, sebagai jejak keputusan.

## 5. Prioritas Penyusunan

Urutan prioritas dokumen: A. Business Plan, B. Model Produk & Layanan, C. Arsitektur Teknis, D. Infrastruktur & Skalabilitas, E. Rencana Operasional, F. Rencana Keuangan, G. RAB, H. Roadmap, I. Analisis Risiko, J. Rencana Implementasi.
