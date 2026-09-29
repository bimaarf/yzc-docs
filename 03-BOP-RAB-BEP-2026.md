# BOP — RAB — BEP Yz-Course 2026-2027

**Tanggal:** 3 September 2026 · **Dipindah ke `docs/business/`:** 29 September 2026 (dari arsip `3-SEPTEMBER-2026/`)
**Lokasi kanonik:** `docs/business/BOP-RAB-BEP-2026.md` (referensi lama `docs/BOP-RAB-2026.md` tidak pernah ada — dikoreksi)
**Status:** ESTIMASI — angka real perlu validasi owner (biaya tutor/home-visit Pontianak/Sambas/Ketapang, transport, komisi)
**Sumber produk:** `tb_product` prod 3 Sept 2026 (20 produk, 599K–2.899K), `liveChatSalesPlaybook.js` 15 SKU, `productList.md`
**Katalog referensi:** `DATA-PRODUK-PROMO-TERBARU.json` (arsip `docs/archived/3-SEPTEMBER-2026/`)

> **Catatan:** Dokumen ini mengisi gap G4 audit (BOP/RAB/BEP tidak ada). Semua angka dalam Rupiah, belum termasuk PPN. Asumsi konservatif Pontianak 2026.

> ## ⚠️ UPDATE 29 September 2026 (verifikasi ulang — angka belum diubah)
> 1. **Directive owner 20 Sep** (`URGENT_OWNER_NO_SIDANG_CAREER_INTERVIEW_20260920`): segmen **Sidang / Interview / Career DITAHAN**. Baris margin/BEP yang memakai paket `Sidang 16` & `Career` **tidak boleh dipakai untuk keputusan baru** sampai owner membuka kembali (lihat header `BUSINESS-MODEL-YZ-2026-2028.md`).
> 2. **Harga Kids di katalog produksi = Rp1.999.000** (`frontend-next/src/lib/productCatalog.js`, dicek 29 Sep) — dokumen ini menghitung Rp1.950.000 → selisih kecil, sinkronkan saat validasi.
> 3. **`Online Reguler 175K` sudah ada di `productCatalog.js`** [terverifikasi 29 Sep] — action item "daftarkan SKU di DB" (§7) bisa dicek status akhirnya.
> 4. Angka fixed cost (server Rp1,2jt / AI Rp600K) tetap **asumsi** — belum ada invoice yang divalidasi.

---

## 1. Asumsi Dasar

| Asumsi | Nilai | Sumber |
|--------|-------|--------|
| Siswa aktif target 2026 | 150 siswa (Q4), 500 siswa (2027) | `roadmap-final:168` trademark 500 |
| Sesi/bulan rata-rata | 8 sesi (Reguler) – 20 sesi (Intensif) | `tb_product` |
| Durasi sesi | 90 menit | `liveChatSalesPlaybook.js:11` |
| Tutor pool | 8–12 tutor freelance Pontianak | Estimasi |
| Home visit coverage | Pontianak kota + Kubu Raya (radius 15km), Sambas/Ketapang via online/hybrid | `liveChatSalesPlaybook.js:400` |
| Platform fee marketplace | 5% | `marketplaceApi.js: fee 5%` |
| Payment gateway Midtrans | 2% + Rp2.000 per transaksi | Midtrans docs |
| AI cost Groq/Morph | Rp400K–800K/bulan (6 provider, 100 query/hari) | `ai_requests.log` avg 1.5K tokens/query |
| Server IDCloudHost 8 vCPU/24GB/20GB swap/100GB SSD | Rp1.200.000/bulan | `docs/INFRASTRUCTURE-LENGKAP.md:90` estimasi IDCloudHost Business |
| R2 storage + CDN | Rp150.000/bulan (yz-cloud bucket) | Estimasi |
| Domain + SSL | Rp300.000/tahun | - |

---

## 2. BOP — Biaya Operasional Pokok (Bulanan)

### 2.1 Fixed Cost (tidak tergantung jumlah siswa)

| Pos | Detail | Estimasi/bulan | Keterangan |
|-----|--------|----------------|------------|
| **Server** | IDCloudHost 8 vCPU/24GB + backup `/mnt/yz-extra` | **1.200.000** | `INFRASTRUCTURE-LENGKAP.md:90` |
| **AI API** | Groq 10 key `V1..V9` + Morph 744B + OpenAI fallback | **600.000** | Avg 3K tokens/query × 2K query/bulan × $0.0004/1K |
| **Storage/CDN** | Cloudflare R2 `yz-cloud` + `cdn.yz-course.com` | **150.000** | - |
| **WA Gateway** | `whatsapp-web.js` di `socket-wa:4002` + nomor 085853964582 | **100.000** | Kuota + perangkat |
| **Domain/SSL** | `yz-course.com` + `app.yz-course.com` | **25.000** | 300K/tahun ÷12 |
| **Admin CS** | 1 admin full-time (chat, follow-up, scheduling) | **2.500.000** | UMR Pontianak 2026 ~2.7jt |
| **Content + SEO** | Writer + `aiContentPublisher.js` + Canva | **800.000** | 8 artikel/bulan |
| **Akuntansi + Legal** | Pembukuan + pajak UMKM | **400.000** | - |
| **Total Fixed** | | **5.775.000** | |

### 2.2 Variable Cost (per siswa/paket)

| Paket Contoh | Harga Jual | Komisi Tutor (45%) | Transport Home-Visit | Materi/AI | Gateway 2% | **Total Var** | **Margin** |
|--------------|------------|--------------------|----------------------|-----------|------------|---------------|------------|
| **Habit Reset 5 sesi** | 599.000 | 269.550 | 75.000 (5×15K) | 10.000 | 13.980 | **368.530** | **230.470 (38%)** |
| **Online Reguler 8 sesi** | 175.000* | 78.750 | 0 (online) | 8.000 | 5.500 | **92.250** | **82.750 (47%)** |
| **Private Starter 8** | 899.000 | 404.550 | 120.000 (8×15K) | 12.000 | 19.980 | **556.530** | **342.470 (38%)** |
| **Kids 20 sesi** | 1.950.000 | 877.500 | 300.000 (20×15K) | 20.000 | 41.000 | **1.238.500** | **711.500 (36%)** |
| **Sidang 16 sesi** | 1.699.000 | 764.550 | 240.000 | 16.000 | 35.980 | **1.056.530** | **642.470 (38%)** |
| **IELTS Foundation 24** | 2.899.000 | 1.304.550 | 360.000 | 24.000 | 59.980 | **1.748.530** | **1.150.470 (40%)** |
| **Duo 6 sesi** | 899.000 | 404.550 (dibagi 2 tutor? 1 tutor) | 90.000 | 10.000 | 19.980 | **524.530** | **374.470 (42%)** |

> *Online Reguler 175K adalah SKU Sprint baru di `liveChatSalesPlaybook.js:6` (slot terbatas, bawa grup 4 orang). DB prod masih 349K untuk SKU lama — pakai 175K untuk hitungan entry, 349K untuk Private Group 20 sesi.

**Catatan komisi:** 45% untuk tutor freelance Pontianak (pasar lokal 40-50%). Home-visit transport 15K/sesi (bensin + parkir). Online = 0 transport.

---

## 3. RAB — Rencana Anggaran Biaya

### 3.1 RAB 14 Hari War Plan (sesuai `yzcourse-growth-war-plan:48` — target 10 checkout)

| Pos | Anggaran 14 hari | Detail |
|-----|------------------|--------|
| **Ads Meta/TikTok** | 1.400.000 | 100K/hari ×14, target 25-40 lead, CPL 35-55K |
| **Konten** | 400.000 | 4 reels + 2 carousel + thumbnail AI `aiContentPublisher.js` |
| **WA blast + Follow-up** | 150.000 | `socket-wa` + `mentor:weekly-checkin` |
| **Fee tutor trial** | 600.000 | 10 trial × 60K |
| **Total RAB 14 hari** | **2.550.000** | |

**Target revenue 14 hari (10 checkout mix):**
- 2× Habit Reset 599K = 1.198M
- 3× Private Starter 899K = 2.697M
- 3× Kids 20 1.95M = 5.85M
- 2× Sidang 16 1.699M = 3.398M
- **Gross 13.143M – Var 6.5M – RAB 2.55M – Fixed prorata 2.887M = Net ~1.2M** (14 hari)

### 3.2 RAB Bulanan (steady state 25-30 siswa baru/bulan)

| Pos | Bulanan | Catatan |
|-----|---------|---------|
| Fixed (2.1) | 5.775.000 | - |
| Variable (30 siswa × avg margin 500K) | 15.000.000 | COGS tutor etc. sudah di margin |
| Marketing (ads 3M + konten 800K) | 3.800.000 | Scale dari 14 hari |
| **Total RAB** | **24.575.000** | |
| **Revenue (30 siswa × avg 1.3M)** | **39.000.000** | Mix paket menengah |
| **Net** | **14.425.000** | Margin ~37% |

### 3.3 RAB Tahunan 2026-2027

| Tahun | Siswa baru | Revenue | RAB | Net | Catatan |
|-------|------------|---------|-----|-----|---------|
| **2026 (4 bulan Sep-Des)** | 80 | 104M | 78M | **26M** | Ramp 20/bulan |
| **2027 (12 bulan)** | 300 | 390M | 295M | **95M** | Steady 25/bulan, 500 active |

---

## 4. BEP — Break Even Point

### 4.1 BEP per Paket (Fixed dialokasikan proporsional)

Rumus: `BEP (siswa) = Fixed / (Harga - Variable)`

| Paket | Margin/siswa | BEP/bulan (Fixed 5.775M) | BEP 14 hari (Fixed 2.887M) |
|-------|--------------|--------------------------|----------------------------|
| Habit Reset | 230.470 | 26 siswa | 13 siswa |
| Online Reguler 175K | 82.750 | 70 siswa | 35 siswa |
| Private Starter | 342.470 | 17 siswa | 9 siswa |
| Kids 20 | 711.500 | 9 siswa | 5 siswa |
| Sidang 16 | 642.470 | 9 siswa | 5 siswa |
| IELTS 24 | 1.150.470 | 6 siswa | 3 siswa |

**Insight:** Paket 175K butuh volume 70/bulan untuk BEP sendirian — tidak efisien solo. Harus jadi **entry funnel** ke Kids/Sidang/IELTS. Paket Kids/Sidang/IELTS BEP paling cepat (5-9 siswa).

### 4.2 BEP Overall (mix aktual)

- **Avg harga jual:** 1.300.000 (mix 30% Habit/Reguler, 40% Starter/Kids, 30% Career/IELTS)
- **Avg variable:** 750.000
- **Avg margin:** 550.000
- **BEP overall:** `5.775.000 / 550.000 = 11 siswa/bulan`

> **Artinya:** Dengan 11 siswa baru/bulan (mix), Yz-Course sudah BEP. Target war plan 10/14 hari = ~20/bulan → sudah di atas BEP. Target 25-30/bulan → profit 37%.

### 4.3 Sensitivitas

| Skenario | Margin | BEP | Net (30 siswa) |
|----------|--------|-----|----------------|
| Komisi tutor 50% (+5%) | 480K | 13 siswa | 8.6M |
| Harga naik 10% (promo off) | 680K | 9 siswa | 14.6M |
| Ads naik 50% (5.7M) | 550K | 11 siswa | 10.6M |
| Home-visit transport naik 20K/sesi | 480K | 13 siswa | 8.6M |

---

## 5. LTV / CAC

| Metrik | Nilai | Hitung |
|--------|-------|--------|
| **CAC** | 95.000 | RAB 14 hari 2.55M ÷ 27 lead (avg war plan 25-40) → 95K/lead, closing 37% → 257K/customer |
| **LTV** | 2.600.000 | Avg 2 paket/customer (Habit 599K → Kids 1.95M), retention via `English Passport` + `AI Mentor WA` |
| **LTV/CAC** | **10.1×** | Sehat (>3×). Jika hanya 1 paket, LTV 1.3M → 5.0× masih sehat |
| **Payback** | 1.2 bulan | CAC 257K ÷ margin 550K/bulan |

---

## 6. Rekomendasi Pricing & Paket (Gap G2/G5)

1. **Single source:** Jadikan `tb_product.key` truth — sync `productList.md` (20) + `liveChatSalesPlaybook.js` (15) + `landingContent.js` + `seo.js` via `buildLiveChatProductContext()` (sudah live 3 Sept). **Daftarkan SKU baru** `Online Reguler 175K` sebagai ID 23 di DB agar DB=Playbook=Landing (sekarang 175K hanya di playbook).
2. **Rename produk DB ke Yz Path™:** `Fun English Kids Starter → Yz Kids • Fun English`, `Speaking Confidence → Yz Speak`, `Career English → Yz Career`, `TOEFL/IELTS Foundation → Yz TOEFL/IELTS` — update `seo.js` & `landingContent.js`.
3. **Promo logic:** DB `12-14%` (prod) vs playbook `12%` vs salesKnowledge `12%` — sudah sinkron 3 Sept via `liveChatAIAgent.js:120` boolean fix. Pertahankan `Promo Kurma 12%` sebagai default, `14%` untuk Speaking/Duo di prod.
4. **Funnel:** Jual `Habit Reset 599K` + `Online Reguler 175K` sebagai entry (BEP tinggi tapi volume), upsell ke `Kids/Sidang` (BEP cepat, margin 36-38%), leverage `IELTS 24` (margin 40%).

---

## 7. Action Plan Owner (validasi angka)

- [ ] Isi biaya tutor real per sesi (45% asumsi) — minta slip 3 bulan terakhir
- [ ] Cek transport home-visit real Pontianak (15K asumsi) — bensin + ojek
- [ ] Konfirmasi server cost IDCloudHost invoice terbaru (1.2M asumsi)
- [ ] Tentukan ads budget 14 hari (1.4M asumsi) — test 100K/hari
- [ ] Set harga final `Online Reguler 175K` di DB (buat ID 23) + update `productList.md`
- [ ] Jalankan `eci-competitor-intelligence-agent.sh` untuk mapping `Superprof/Kampung Inggris Pontianak/Sigma/EF` vs Yz (harga, funnel, trust moat) — tutup gap G4

---

*Estimasi konservatif — BEP 11 siswa/bulan, net 37% di 30 siswa/bulan. Angka real akan lebih akurat setelah 1 bulan war plan dengan data `marketplace_transactions` fee 5% + `ai_usage` cost. Dokumen ini hidup — update tiap sprint via `YZ_BRIDGE_BOARD.md`.*
