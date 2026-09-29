# 🏗️ INFRASTRUKTUR PRODUCTION YZ-COURSE (per 29 September 2026)

**Status:** TERVERIFIKASI dari repo + cek live (bukan estimasi) — namun beberapa item ditandai *perlu tindak lanjut*.
**Sumber:** `docker-compose.yml`, `nginx-config-production` (update file: 3 Mei 2026 — waspada drift), `socket-server/ecosystem.config.cjs`, `docker-compose.ai-tutor.local.yml`, cek `curl` live 29 Sep, log relay server (29 Sep).
**Server produksi:** `[server produksi — alamat IP tidak dipublikasikan]` — root site `/var/www/yz-course.com`.
**Deep-dive historis:** `docs/archived/8-AUGUST-2026/INFRASTRUCTURE-LENGKAP.md` (update 30 Agu 2026).

## 1) Routing publik — VERIFIKASI LIVE 29 Sep
| Domain | Kondisi repo (nginx config) | Hasil cek live 29 Sep |
|---|---|---|
| `yz-course.com` / `www` | `www` → 301 ke apex; lalu proxy API/Tool (socket-wa 4002, AI 4003, SD 4004, WebRTC 4012, Laravel php-fpm) + konten dari disk | ✅ **200 — melayani Next.js STATIC EXPORT dari disk** (chunk `/_next/static`, header static, `last-modified` build **13 Sep 2026**) |
| `app.yz-course.com` | Next.js SSR `:3001` (proxy `@next_app`) | 🔴 **502 — SSR produksi tidak merespons saat dicek** → tindak lanjut lane server |

Route API (dari `nginx-config-production`, berlaku di domain publik):
`/socket-wa/*` → :4002 · `/api/v2/*`, `/api/blog/`, `/api/chat/` → :4002 · `/api/ai/` → :4003 · `/api/sd/`, `/api/ai-chat/` → :4004 · `/api/v1/api/ai-webrtc/*` → rewrite → :4012 · `/api/v1/api/*` + `/graphql` → PHP-FPM 8.4 (Laravel) · `/api/v1/storage/*` → disk.

## 2) Docker compose — services & port host (verified dari `docker-compose.yml`)
| Service | Container | Port host → dalam |
|---|---|---|
| postgres (PG16+pgvector) | yz-course-postgres | 5434 → 5432 |
| postgres-replica | yz-course-postgres-replica | 5435 → 5432 |
| redis | yz-course-redis | 6380 → 6379 |
| laravel | yz-course-laravel | 8000 → 8000 |
| nginx (mode compose) | yz-course-nginx | 3006 → 80 |
| socket-wa (WA + Socket.IO) | yz-course-socket-wa | 4002 → 4002 |
| frontend-next (build prod `node server.js`) | yz-course-frontend-next | **tanpa publish host** (internal) |
| pgadmin | yz-course-pgadmin | 8081 → 80 |
| ollama | yz-course-ollama | 11435 → 11434 |
| prometheus | yz-course-prometheus | 9091 → 9090 |
| postgres-exporter / redis-exporter | — | 9187 / 9121 |
| grafana | yz-course-grafana | 3005 → 3000 |
| sd-webui (A1111 CPU) | yz-course-sd-webui | 7860 → 7860 |

## 3) PM2 (`socket-server/ecosystem.config.cjs`)
| App | Port |
|---|---|
| SOCKET-WA (WhatsApp + Socket.IO) | 4002 |
| AI-WORKER | 4003 |
| WEBRTC-AI-AGENT (Tutor voice) | 4012 |
| CODEX-CLASSROOM-AI-SUPERVISOR | — (background) |

## 4) AI / Tutor Voice (stack terbaru Sep 2026)
- **STT:** whisper-cpp `ggml-base.bin` (`WHISPER_THREADS=3`, `-bs 1 -l id`, spawn non-blocking)
- **TTS berlapis:** Edge TTS **(default, gratis)** → OpenAI TTS (opsional `TUTOR_TTS_PRIMARY=openai`, `gpt-4o-mini-tts`→`tts-1-hd`, circuit-breaker 10 menit) → Google TTS → null
  - Voice ID default: `en-US-AvaMultilingualNeural` ("ala GPT") + prosodi +18%/+8Hz/+6%; EN: `en-US-EmmaNeural`
- **Realtime:** VAD 450ms (`VAD_SILENCE_MS`), queue maks 2, barge-in `speech_started`, resume `resume_session_id` (TTL detach 10 menit), RAG budget 700ms, emoji dibuang untuk TTS
- Override lokal `docker-compose.ai-tutor.local.yml`: `WHISPER_CPP_BIN=/usr/local/bin/whisper-cpp`, `EDGE_TTS_BIN=/opt/edge-tts/bin/edge-tts`; limit `socket-wa` CPU 3.0 / mem 2G

## 5) Storage / CDN / SSL
- Cloudflare **R2** bucket `yz-cloud` + CDN `cdn.yz-course.com`
- SSL: LetsEncrypt `app.yz-course.com`; `/etc/ssl/yz-course/*` untuk `yz-course.com`

## 6) Monitoring
Prometheus (9090→9091), Grafana (3000→3005), postgres_exporter, redis_exporter.

## 7) Automation di server produksi
- **SEO permanent agent** (start 29 Sep 10:35 UTC): interval **7200s**; audit URL smoke/sitemap/content/media/forum; gate provider **blocked** (Encited 🔑 missing, gate disabled; Cloudflare purge gate enabled tapi **mutasi dimatikan**).
- **Dawn Index Rush / Encited runner:** hold di luar reset window Cloudflare — **tanpa mutasi**.
- **Bridge relay server → Codex lokal:** snapshot ke `/tmp/yz-server-bridge-latest.md` + broadcast `/tmp/yz-local-codex-broadcast.md` (sempat `ssh_or_stat_failed`, transient).
- Secrets agent: disimpan di **secret store server** (tidak dipublikasikan; jangan pernah di-print).

## 8) Lokal (dev) vs Produksi — jangan tertukar
| | Lokal | Produksi |
|---|---|---|
| `:3001` | **Host dev server** (`next dev --turbo -p 3001`, log `/tmp/yz-frontend-dev.out`) | Container `frontend-next` (build prod) **tidak publish port**; SSR diakses internal/proxy |
| `yz-course.com` | — | Static export Next di disk; `app.yz-course.com` = SSR :3001 |

## 9) Perlu tindak lanjut (jujur — belum selesai)
1. 🔴 `app.yz-course.com` → 502 (SSR produksi) — cek & hidupkan `:3001` di server.
2. Sinkronkan `nginx-config-production` repo vs config server aktual (file repo terakhir update 3 Mei; live sudah berubah).
3. Invoice server IDCloudHost (8 vCPU/24GB) & R2 — untuk memvalidasi angka BOP/RAB [A].
4. Gate Encited (API key) — menunggu owner; sampai itu, refresh Encited/Index Rush tetap dimatikan.
