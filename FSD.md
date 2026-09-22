# FSD — KosManager (lite)

## Arsitektur

API: ASP.NET Core 8, Clean Architecture-lite 4 proyek
(Domain → Application → Infrastructure → Api). Web: Blazor Server + MudBlazor
mengonsumsi REST API (JWT). DB: MySQL 8 (EF Core + migrasi + seed fiktif).

## Fungsional per endpoint

| Endpoint | Role | Aturan |
|---|---|---|
| `POST /api/auth/register` | publik | hanya role penghuni |
| `POST /api/auth/login` | publik | 401 bila salah |
| `GET /api/auth/me` | login | — |
| `GET /api/rooms` | login | + nama penghuni |
| `POST/PUT/DELETE /api/rooms` | owner | — |
| `GET /api/tenants` (+import CSV ≤2MB) | owner | import lapor imported/failed |
| `POST/PUT/DELETE /api/tenants` | owner | ganti kamar → status isi |
| `GET /api/bills[?status]` | owner semua / penghuni miliknya | + daysLate |
| `POST /api/bills/generate?periode=` | owner | idempoten, tenor tgl-10 |
| `POST /api/payments` | owner / miliknya | bill → pending |
| `POST /api/payments/{id}/verify` | owner | approve → paid |
| `GET /api/payments/queue` | owner | belum verified |
| `GET /api/dashboard` | owner | okupansi, kas, tunggakan, overdue, reminders |
| `GET /api/dashboard/report.csv` | owner | header penghuni,periode,... |
| `GET /api/dashboard/trend` | owner | kas + tunggakan 6 bulan terakhir |
| `GET /api/bills/{id}/receipt.pdf` | owner / miliknya | QuestPDF, stempel LUNAS/BELUM |
| `POST /api/notify/test` | owner | mock/telegram via `INotificationSender` |

## Scheduler

`ReminderService` (BackgroundService, tiap jam): H-3/H-1/H+1, skip tanpa
chat_id, tulis `notification_logs`, idempoten via `reminded_stage`.

## Keamanan

JWT 24h + policy owner/penghuni · BCrypt · secret via user-secrets/env
(fail-fast) · CI secret dummy · tanpa secret di git.
