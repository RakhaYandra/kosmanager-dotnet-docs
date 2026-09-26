# SRS -- KosManager (IEEE 830)

## 1. Pendahuluan

### 1.1 Tujuan

Menetapkan kebutuhan API + web kos single-properti ($0, repo publik aman)
sebagai acuan implementasi dan uji.

### 1.2 Ruang Lingkup

MVP + Fase 2a (struk PDF, grafik kas). Di luar lingkup: denda otomatis,
QRIS, multi-kos, dark mode, webhook publik (lihat PRD Non-goals).

### 1.3 Definisi & Singkatan

RBAC (role-based access control) * tenor (tanggal jatuh tempo, tgl-10) *
stage (H-3/H-1/H+1) * `reminded_stage` (penanda idempotensi reminder) *
seed fiktif (data contoh, bukan data nyata) * verified-local (terbukti di
mesin dev) * verified-real (terbukti ke layanan asli, mis. Telegram HP).

### 1.4 Referensi

BRD.md * PRD.md (US-01..US-11) * FSD.md (FS-01..FS-18) * ADR-002 (BE) *
ADR-003/ADR-004 (FE).

### 1.5 Overview

S2 konteks * S3 kebutuhan (antarmuka, fungsional, non-fungsional) *
S4 glosarium * S5 batasan * S6 traceability.

## 2. Deskripsi Umum

### 2.1 Perspektif Produk

Sistem mandiri: Blazor -> REST API -> MySQL; scheduler internal; notifikasi
keluar via Telegram/Fonnte; analitik via snapshot DuckDB.

### 2.2 Karakteristik Pengguna

Owner (1 orang, paham spreadsheet) * Penghuni (HP + Telegram opsional).

### 2.3 Lingkungan Operasi

Lokal/dev: Docker MySQL 8.4, .NET 8, browser modern. Tanpa server produksi.

### 2.4 Batasan

$0 * repo publik (tanpa data nyata/secret) * scheduler lokal * teks Indonesia.

## 3. Kebutuhan Khusus

### 3.1 Kebutuhan Antarmuka Eksternal

| ID | Kebutuhan |
|---|---|
| FR-INT-01 | API REST JSON; error `{error}` + kode status terdokumentasi (FSD). |
| FR-INT-02 | Web membaca base URL dari `API_URL` dan mengirim `Authorization: Bearer`. |
| FR-INT-03 | ETL read-only terhadap DB operasional, menulis DuckDB terpisah. |
| FR-INT-04 | Notifikasi keluar via Bot API Telegram / Fonnte (driver ganti). |

### 3.2 Kebutuhan Fungsional

| ID | Kebutuhan |
|---|---|
| FR-AUTH-01 | Register publik hanya role penghuni; duplikat 409. |
| FR-AUTH-02 | Login JWT 24h; salah 401. |
| FR-ROOM-01 | CRUD kamar (nomor unik) + occupancy. |
| FR-TEN-01 | CRUD penghuni + CSV import (maks 2MB, lapor gagal). |
| FR-BILL-01 | Generate bulanan idempoten, tenor tgl-10. |
| FR-BILL-02 | List + filter status + daysLate; penghuni hanya miliknya. |
| FR-BILL-03 | Struk PDF per tagihan (stempel LUNAS/BELUM; owner/miliknya). |
| FR-PAY-01 | Bayar manual -> pending; verifikasi owner -> paid/unpaid + antrean. |
| FR-DASH-01 | Okupansi, kas, tunggakan + hari telat; CSV; tren kas 6 bulan. |
| FR-NTF-01 | Reminder H-3/H-1/H+1 sekali per tagihan; skip tanpa chat_id. |
| FR-NTF-02 | Polling getUpdates/10 dtk (offset file): `/start <email>` tautkan, `SUDAH` catat pending; redelivery idempoten. |

### 3.3 Kebutuhan Non-Fungsional

| ID | Kebutuhan |
|---|---|
| FR-SEC-01 | Tanpa secret di repo (grep bersih); BCrypt; fail-fast config. |
| FR-PERF-01 | Response <500ms lokal; read ter-cache (dash 60 dtk, bills/queue 30 dtk); MiniProfiler. |
| FR-QLT-01 | Newman 25/25, QA 54/54, e2e 12/12 tiap rilis (angka mengikuti repo qa). |

## 4. Glosarium

Tenor * stage * verified-local/real * seed fiktif * idempoten * RBAC --
lihat S1.3.

## 5. Asumsi & Dependensi

MySQL 8.4 Docker * .NET 8 SDK * QuestPDF Community (legal: individu/OSS) *
Telegram gratis (user /start dulu) * Fonnte free-tier cadangan.

## 6. Traceability

FR-AUTH-*->TC-AUTH-* * FR-ROOM-*->TC-ROOM-* * FR-TEN-*->TC-TEN-* *
FR-BILL-*->TC-BILL-* * FR-PAY-*->TC-PAY-* * FR-DASH-*->TC-DASH-* *
FR-NTF-*->TC-NOTIFY-01..09 * FR-SEC/QLT/PERF->TC-SEC-*/CI.
