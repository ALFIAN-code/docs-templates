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
