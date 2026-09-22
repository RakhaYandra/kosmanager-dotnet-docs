# PRD — KosManager MVP (lite)

## Pengguna & peran

- **Owner**: semua fitur. **Penghuni**: tagihanku + bayar.

## User stories (MVP)

1. Sebagai owner saya generate tagihan 1 bulan dalam 1 klik.
2. Sebagai owner saya verifikasi pembayaran (Setuju/Tolak).
3. Sebagai penghuni saya lihat tagihanku + tekan SUDAH BAYAR.
4. Sebagai sistem saya kirim reminder H-3/H-1/H+1 via Telegram, sekali per tagihan.
5. Sebagai owner saya lihat okupansi, kas, tunggakan + hari telat.
6. Sebagai owner saya kelola kamar/penghuni dari web (tambah/ubah/hapus + import CSV).
7. Sebagai penghuni saya daftar sendiri (register) tanpa bantuan owner.
8. Sebagai owner saya unduh rekap CSV + filter tagihan per status (chips).

## Kriteria terima (ringkas)

- Generate idempoten (periode sama 2x → kedua 0).
- Penghuni tak bisa akses data penghuni lain (403) — diuji TC-BILL-02/TC-PAY-02.
- Reminder tak duplikat (kolom `reminded_stage`) — diuji TC-NOTIFY-03.
- Kontrak API di `postman_collection.json` (Newman 22/22).
- Web full coverage 17/17 endpoint (terverifikasi Playwright 9 aksi UI).

## Non-goals MVP

Denda otomatis, struk PDF, QRIS, multi-kos, grafik, dark mode, webhook publik.
