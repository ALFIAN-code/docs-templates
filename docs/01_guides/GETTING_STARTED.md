# Getting Started

> Panduan setup project untuk developer manusia maupun AI agent. AI baca ini sebelum menjalankan command apa pun.

**Terakhir diupdate:** [YYYY-MM-DD]

## Prasyarat

| Kebutuhan | Versi minimal | Cara cek |
|---|---|---|
| [Node.js / Flutter SDK / PHP] | | `node -v` / `flutter --version` / `php -v` |
| Database | | |
| [Lainnya] | | |

## Install

```bash
# [isi command install, misal:]
# npm install
# flutter pub get
# composer install
```

## Setup Environment

1. Copy `.env.example` → `.env` (atau `.env.local`)
2. Isi variable wajib (lihat `ARCHITECTURE.md` > Environment Variables Penting):
   ```
   DATABASE_URL=
   API_KEY=
   ```
3. [Langkah lain, misal: setup Firebase, Moodle config.php]

## Seed / Data Awal

```bash
# [isi, misal:]
# npm run seed
# php admin/cli/install_database.php
```

Akun default untuk dev:
- Email: [isi]
- Password: [isi]

## Menjalankan Project

| Perintah | Fungsi | Command |
|---|---|---|
| Dev | Jalankan lokal | [isi, misal: `npm run dev`, `flutter run`] |
| Test | Jalankan test | [isi] |
| Lint | Cek format | [isi] |
| Build | Build production | [isi] |
| Migrate | Migrasi DB | [isi] |

## Verifikasi Setup Berhasil

- [ ] `GET /health` atau halaman login bisa dibuka
- [ ] Login dengan akun default berhasil
- [ ] Tidak ada error di linter

## Troubleshooting Umum

| Masalah | Solusi |
|---|---|
| [error X] | [solusi] |
| | |

> Jika AI menemukan langkah setup yang tidak tertulis di sini tapi dibutuhkan, usulkan update ke file ini (tanya dulu di L1).
