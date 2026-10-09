# Konvensi Pengembangan

> Aturan penulisan kode, naming, commit, dan pattern. AI wajib patuh. Jika ada yang spesifik per stack, taruh di `docs/stacks/*.md` dan rujuk dari sini.

**Terakhir diupdate:** [YYYY-MM-DD]

## Bahasa

- Kode: Inggris (variable, function, class)
- Dokumen `docs/` : Indonesia
- Komentar: Indonesia boleh untuk logic domain, Inggris untuk generic

## Naming

| Elemen | Aturan | Contoh |
|---|---|---|
| File | `snake_case` atau sesuai stack (Flutter: `snake_case.dart`) | `user_service.dart` |
| Class | `PascalCase` | `UserService` |
| Function/var | `camelCase` (JS/TS/Dart) / `snake_case` (PHP/Moodle) | `getUserById()` |
| Tabel DB | `snake_case`, plural | `users`, `order_items` |
| Kolom DB | `snake_case` | `created_at` |

## Dokumentasi & Log

- `docs/03_logs/PROGRESS_LOG.md` bersifat **append-only**: tambah entry baru di paling atas, jangan pernah edit/timpa entry lama.
- Setiap entry wajib dua baris identitas dari mesin, bukan dari ingatan:
  - stamp `## [YYYY-MM-DD HH:mm]` dari `date "+%Y-%m-%d %H:%M"`.
  - baris `**Kontributor:**` dari `git config user.name`.
- Ambil keduanya dalam satu perintah bash: `date "+%Y-%m-%d %H:%M"; git config user.name`.
- Dilarang menyalin stamp/kontributor dari entry sebelumnya.
- Laporan progress untuk stakeholder disusun dari **gabungan** `PROGRESS_LOG.md` (konteks fitur) + `git log` (atribusi siapa), bukan salah satu saja.
- Format laporan progress ke stakeholder: satu list, tiap baris diawali prefix fitur `[Nama Fitur]`, bahasa non-teknis, tanda `✅` untuk selesai di atas dan `⏳` untuk pending di bawah. Jangan tulis "selesai" yang duplikat `✅`.

## Format & Lint

- Formatter: [isi, misal: `dart format`, `prettier`, `php-cs-fixer`]
- Linter: [isi command, misal: `flutter analyze`, `eslint`]
- AI wajib jalankan linter sebelum klaim selesai (jika ada di `GETTING_STARTED.md`).

## Commit Message

Format: `[tipe] deskripsi singkat`

Tipe: `feat`, `fix`, `docs`, `refactor`, `chore`

Contoh: `feat: tambah filter periode di analytics`

## Pattern Wajib

- [Misal: "Semua API response pakai wrapper `{success, data, message}`"]
- [Misal: "Validasi input di layer service, bukan controller"]
- [Misal: "Jangan hardcode string UI, pakai file `l10n/*.json`"]

## Pattern yang Dilarang

- [Misal: "Jangan pakai `any` di TypeScript"]
- [Misal: "Jangan query langsung di widget Flutter, pakai provider/repository"]

## Handling Error & Log

- [Aturan log, misal: "pakai `logger.info` bukan `print`"]

## Catatan untuk AI Agent

- Jika task meminta sesuatu yang melanggar konvensi ini, konfirmasi dulu dan catat di `DECISIONS.md` jika disetujui untuk dilanggar.
- Aturan spesifik stack (misal: Moodle `upgrade.php` step) ada di `docs/stacks/*.md` — baca itu juga.
