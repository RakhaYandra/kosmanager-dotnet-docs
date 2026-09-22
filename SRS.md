# SRS — KosManager (lite, ringkas IEEE-style)

## 1. Pendahuluan

Tujuan: API + web kos single-properti, $0, repo publik aman.
Lingkup: MVP (lihat PRD). Definisi: RBAC, tenor, stage reminder.

## 2. Kebutuhan fungsional

- FR-01 Auth JWT 2 role; register publik hanya penghuni (+ halaman /register di web).
- FR-02 CRUD kamar via API + web (dialog, nomor unik) + occupancy.
- FR-03 CRUD penghuni via API + web + CSV import via UI (maks 2MB, lapor gagal).
- FR-04 Generate tagihan bulanan idempoten, tenor tgl-10.
- FR-05 Pembayaran manual + verifikasi owner (paid/unpaid).
- FR-06 Dashboard: okupansi, kas, tunggakan + hari telat.
- FR-07 Reminder H-3/H-1/H+1 Telegram (mock default), sekali per tagihan.
- FR-08 Laporan CSV bulanan via API + tombol Unduh di dashboard.
- FR-09 Web full coverage 17/17 endpoint; filter Tagihan = chips pill.
- FR-10 Struk PDF per tagihan (QuestPDF Community; owner atau miliknya).
- FR-11 Grafik kas 6 bulan (`/api/dashboard/trend` + MudChart).

## 3. Kebutuhan non-fungsional

- NFR-01 Tanpa secret di repo (grep bersih).
- NFR-02 Response API <500ms di lokal; read ter-cache (dashboard 60 dtk, bills/queue 30 dtk) + MiniProfiler `/profiler/results`.
- NFR-03 Seed 100% fiktif.
- NFR-04 Newman 22/22, QA 47/47, e2e 12/12 tiap rilis.

## 4. Traceability (ringkas)

FR-01→TC-AUTH-* · FR-02→TC-ROOM-* · FR-03→TC-TEN-* · FR-04→TC-BILL-*
FR-05→TC-PAY-* · FR-06→TC-DASH-* (inkl. TC-DASH-05 tren) · FR-07→TC-NOTIFY-* · FR-08/FR-09→UI 9/9 · FR-10→TC-BILL-09/10 · NFR→TC-SEC-*/CI.

## 5. Keputusan arsitektur

ADR-002 (BE CA-lite) di repo API · ADR-003 (FE CA-ish) + ADR-004 (frontend fixes) di repo web.
