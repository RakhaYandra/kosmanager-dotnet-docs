# PRD -- KosManager

## Pengguna & peran

- **Owner**: semua fitur. **Penghuni**: tagihanku + bayar.

## User stories

| ID | Story | Status |
|---|---|---|
| US-01 | Sebagai owner saya generate tagihan 1 bulan dalam 1 klik. | Done |
| US-02 | Sebagai owner saya verifikasi pembayaran (Setuju/Tolak). | Done |
| US-03 | Sebagai penghuni saya lihat tagihanku + tekan SUDAH BAYAR. | Done |
| US-04 | Sebagai sistem saya kirim reminder H-3/H-1/H+1 via Telegram, sekali per tagihan. | Done |
| US-05 | Sebagai owner saya lihat okupansi, kas, tunggakan + hari telat. | Done |
| US-06 | Sebagai owner saya kelola kamar/penghuni dari web (tambah/ubah/hapus + import CSV). | Done |
| US-07 | Sebagai penghuni saya daftar sendiri (register) tanpa bantuan owner. | Done |
| US-08 | Sebagai owner saya unduh rekap CSV + filter tagihan per status (chips). | Done |
| US-09 | Sebagai owner/penghuni saya unduh struk PDF per tagihan (stempel LUNAS/BELUM). | Done |
| US-10 | Sebagai owner saya lihat grafik kas 6 bulan di dashboard. | Done |

## Kriteria terima (ringkas)

- Generate idempoten (periode sama 2x -> kedua 0).
- Penghuni tak bisa akses data penghuni lain (403) -- diuji TC-BILL-02/TC-PAY-02/TC-BILL-10.
- Reminder tak duplikat (kolom `reminded_stage`) -- diuji TC-NOTIFY-03.
- Kontrak API di `postman_collection.json` (Newman 25/25).
- Web full coverage 17/17 endpoint (terverifikasi Playwright 9 aksi UI).
- Struk valid `%PDF` + tren konsisten dashboard (TC-BILL-09, TC-DASH-05).

## Non-goals (Fase 2b)

Denda otomatis, QRIS, multi-kos, dark mode, webhook publik.
