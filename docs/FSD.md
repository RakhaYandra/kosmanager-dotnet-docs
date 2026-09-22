# FSD — KosManager

## Arsitektur

API: ASP.NET Core 8, Clean Architecture-lite 4 proyek
(Domain → Application → Infrastructure → Api). Web: Blazor Server + MudBlazor
mengonsumsi REST API (JWT). DB: MySQL 8 (EF Core + migrasi + seed fiktif).
Cache: `AsNoTracking` + `IMemoryCache` (TTL 30-60 dtk, invalidasi per prefix);
MiniProfiler di `/profiler/results`.

## Fungsional per endpoint

| ID | Endpoint | Role | Aturan |
|---|---|---|---|
| FS-01 | `POST /api/auth/register` | publik | hanya role penghuni |
| FS-02 | `POST /api/auth/login` | publik | 401 bila salah |
| FS-03 | `GET /api/auth/me` | login | — |
| FS-04 | `GET /api/rooms` | login | + nama penghuni (cached 60 dtk) |
| FS-05 | `POST/PUT/DELETE /api/rooms` | owner | invalidate rooms/tenants/dash/bills |
| FS-06 | `GET /api/tenants` (+import CSV ≤2MB) | owner | import lapor imported/failed |
| FS-07 | `POST/PUT/DELETE /api/tenants` | owner | ganti kamar → status isi |
| FS-08 | `GET /api/bills[?status]` | owner semua / penghuni miliknya | + daysLate (cached 30 dtk, key per tenant) |
| FS-09 | `POST /api/bills/generate?periode=` | owner | idempoten, tenor tgl-10 |
| FS-10 | `POST /api/payments` | owner / miliknya | bill → pending |
| FS-11 | `POST /api/payments/{id}/verify` | owner | approve → paid |
| FS-12 | `GET /api/payments/queue` | owner | belum verified (cached 30 dtk) |
| FS-13 | `GET /api/dashboard` | owner | okupansi, kas, tunggakan, overdue, reminders (cached 60 dtk) |
| FS-14 | `GET /api/dashboard/report.csv` | owner | header penghuni,periode,... |
| FS-15 | `GET /api/dashboard/trend` | owner | kas + tunggakan 6 bulan terakhir |
| FS-16 | `GET /api/bills/{id}/receipt.pdf` | owner / miliknya | QuestPDF Community, stempel LUNAS/BELUM |
| FS-17 | `POST /api/notify/test` | owner | mock/telegram via `INotificationSender` |

## Scheduler

`ReminderService` (BackgroundService, tiap jam): H-3/H-1/H+1, skip tanpa
chat_id, tulis `notification_logs`, idempoten via `reminded_stage`.

## Keamanan

JWT 24h + policy owner/penghuni · BCrypt · secret via user-secrets/env
(fail-fast) · CI secret dummy · tanpa secret di git.
