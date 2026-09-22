# BRD -- KosManager

## 1. Latar belakang

Pemilik kos single-properti menagih manual via chat: jatuh tempo lupa,
tunggakan tak tercatat, bukti bayar terserak. Skala: 1 kos, 5-30 kamar.

## 2. Tujuan bisnis

- Nol tagihan terlewat tanpa pengingat (H-3/H-1/H+1 otomatis).
- Tunggakan terpantau nominal + hari telat per penghuni.
- Setiap tagihan punya struk PDF; kas terpantau grafik 6 bulan.
- Biaya operasional $0 (tanpa server, tanpa gateway berbayar).

## 3. Stakeholder

Owner (kelola penuh) * Penghuni (lihat + bayar tagihannya) * (Fase 2: multi-kos).

## 4. Kebutuhan tingkat tinggi

| ID | Kebutuhan | Prioritas | Status |
|---|---|---|---|
| BR-01 | Kamar + status hunian terpantau | Must | Done |
| BR-02 | Tagihan bulanan otomatis, tenor tgl-10 | Must | Done |
| BR-03 | Bayar manual + verifikasi owner | Must | Done |
| BR-04 | Reminder Telegram otomatis | Must | Done |
| BR-05 | Dashboard tunggakan + laporan CSV | Must | Done |
| BR-06 | Struk PDF per tagihan | Must | Done (Fase 2a) |
| BR-07 | Grafik kas 6 bulan | Should | Done (Fase 2a) |
| BR-08 | Denda/QRIS/multi-kos | Won't | Fase 2b |

## 5. Batasan

Repo publik (tanpa data nyata) * tanpa deploy (scheduler lokal) * $0.
