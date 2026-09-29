# 📚 Dokumen Bisnis & Operasional — Yz-Course

Kumpulan dokumen **bisnis, strategi, keuangan (BOP/RAB/BEP), pricing, dan infrastruktur produksi** Yz-Course — referensi internal yang terstruktur dan siap dipublikasikan.

- **Organisasi:** Yz-Course — kursus Bahasa Inggris (Pontianak & Kalimantan Barat)
- **Terakhir diperbarui:** 29 September 2026
- **Sifat dokumen:** ringkasan strategis & audit. Setiap angka diberi label `[F]` fakta bersumber · `[A]` asumsi yang perlu validasi · `[?]` tidak ditemukan.
- **Keamanan:** seluruh dokumen telah **disanitasi** — tidak memuat kredensial, alamat IP server, maupun token.

## Daftar Dokumen

| # | Dokumen | Isi | Status |
|---|---|---|---|
| 01 | [`01-BUSINESS-MODEL-YZ-2026-2028.md`](01-BUSINESS-MODEL-YZ-2026-2028.md) | Business plan (deep research 15 langkah + The Big Bet) — 20 Sep 2026 | ✅ Aktif — perhatikan header directive (segmen tertentu ditahan) |
| 02 | [`02-VISION-POSITIONING-2026-2027.md`](02-VISION-POSITIONING-2026-2027.md) | Visi & positioning resmi — 4 Sep 2026 | ✅ Aktif |
| 03 | [`03-BOP-RAB-BEP-2026.md`](03-BOP-RAB-BEP-2026.md) | BOP, RAB, BEP, LTV/CAC — 3 Sep 2026 | ⚠️ Estimasi — perlu validasi angka |
| 04 | [`04-INFRASTRUKTUR-PRODUCTION-2026-09.md`](04-INFRASTRUKTUR-PRODUCTION-2026-09.md) | Infrastruktur produksi terverifikasi (services, routing, AI voice stack, otomasi) | ✅ 29 Sep 2026 |
| 05 | [`05-PRICING-AUDIT-2026-09-29.md`](05-PRICING-AUDIT-2026-09-29.md) | Audit konsistensi harga lintas kanal (listing vs database vs live chat) | 🔎 1 temuan kritis |
| 06 | [`06-PLAN-SEO-AGENT-2026.md`](06-PLAN-SEO-AGENT-2026.md) | Rencana kerja agent SEO (aktif berjalan di server, siklus ±2 jam) | ✅ Live |
| 07 | [`07-PRE-PRODUCTION-AUDIT-2026-09-29.md`](07-PRE-PRODUCTION-AUDIT-2026-09-29.md) | Audit pra-rilis, build produksi, deploy, dan perbaikan insiden (termasuk perbaikan deteksi bahasa STT) | ✅ 29 Sep 2026 |
| 📦 | [`arsip/`](arsip/) | Dokumen arsip — tidak aktif namun disimpan untuk jejak keputusan | 📦 Arsip |

## Ringkasan Status Produksi (per 29 September 2026)

**Selesai**
- ✅ Build produksi sukses dan **ter-deploy** (BUILD_ID baru aktif di server)
- ✅ Health check seluruh layanan produksi = 200 (web, socket, AI worker, WebRTC agent)
- ✅ Perbaikan deteksi bahasa STT — transkripsi Bahasa Indonesia kini akurat
- ✅ Audit keamanan promo — voucher pengujian **nonaktif** di database produksi

**Terbuka (perlu keputusan / penanganan lanjutan)**
- SKU *Duo Speaking Sprint* tampil di listing namun belum terdaftar di database produksi
- Kebijakan promo belum bersumber tunggal (multi-sistem)
- Subdomain aplikasi (`app.*`) mengembalikan 502 — perlu penanganan
- Validasi angka BOP/RAB dengan data operasional nyata

## Konvensi Penulisan
- Setiap dokumen memuat **tanggal** dan **sumber** di bagian atas.
- Angka wajib berlabel `[F]` / `[A]` / `[?]`.
- Dokumen historis dipindahkan ke `arsip/` — tidak dihapus.
