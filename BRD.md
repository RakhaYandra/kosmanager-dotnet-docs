# BRD — KosManager (lite)

## 1. Latar belakang

Pemilik kos single-properti menagih manual via chat: jatuh tempo lupa,
tunggakan tak tercatat, bukti bayar terserak. Skala: 1 kos, 5-30 kamar.

## 2. Tujuan bisnis

- Nol tagihan terlewat tanpa pengingat (H-3/H-1/H+1 otomatis).
- Tunggakan terpantau nominal + hari telat per penghuni.
- Biaya operasional $0 (tanpa server, tanpa gateway berbayar).

## 3. Stakeholder

Owner (kelola penuh) · Penghuni (lihat + bayar tagihannya) · (Fase 2: multi-kos).

## 4. Kebutuhan tingkat tinggi

| ID | Kebutuhan | Prioritas |
|---|---|---|
| BR-01 | Kamar + status hunian terpantau | Must |
| BR-02 | Tagihan bulanan otomatis, tenor tgl-10 | Must |
| BR-03 | Bayar manual + verifikasi owner | Must |
| BR-04 | Reminder Telegram otomatis | Must |
| BR-05 | Dashboard tunggakan + laporan CSV | Must |
| BR-06 | Denda/struk PDF/QRIS | Won't (Fase 2) |

## 5. Batasan

Repo publik (tanpa data nyata) · tanpa deploy (scheduler lokal) · $0.
