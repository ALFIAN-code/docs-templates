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

- **Page Shell & Navigation:** Halaman wajib dibungkus dengan `NdScaffold`, header menggunakan `NdAppBar`, tombol aksi di AppBar menggunakan `NdAppBarButton`, dan tombol aksi bawah halaman menggunakan `SharedBottomActionBarWidget`.
- **Localization:** Semua teks UI wajib menggunakan helper localization `context.t('module.section.key')`, dilarang hardcode string literal di widget.
- **Theme & Tokens:** Semua styling warna, spacing, dan radius wajib melalui `final t = NedoThemeData.of(context);` (akses `t.color*`, `t.spacing*`, `t.radius*`).
- **Card Decoration:** Semua kontainer kartu/panel wajib menggunakan `decoration: t.cardDecoration(...)` dari `app_card_theme.dart`.
- **API Response:** Semua API response menggunakan wrapper standar `{success, data, meta, error}` (lihat `02_reference/API_STYLE.md`).
- **Clean Architecture:** Validasi dan logic bisnis di layer domain/service/usecases, bukan di widget presentation.

## Pattern yang Dilarang

- **Dilarang memakai `Scaffold` atau `AppBar` dari `material.dart` langsung** di modul halaman — wajib gunakan `NdScaffold` dan `NdAppBar`.
- **Dilarang membuat kontainer tombol manual** di AppBar actions — wajib gunakan `NdAppBarButton` agar styling seragam dengan tombol back.
- **Dilarang hardcode teks UI mentah** (bahasa Indonesia/Inggris) langsung di widget — wajib gunakan `context.t(...)`.
- **Dilarang hardcode warna** (`Color(0xFF...)` atau `Colors.blue`) di widget — wajib gunakan token tema `t.*`.
- **Dilarang membuat `BoxDecoration` manual** untuk kartu — wajib `t.cardDecoration(...)`.
- **Dilarang menduplikasi widget** hanya karena beda padding/warna — gunakan parameter varian (`type`/`variant`) atau parameter opsional.
- **Dilarang logic bisnis di UI widget** — widget `presentation` hanya bertanggung jawab untuk render tampilan dan event handling.
- **Dilarang query / call API langsung di widget presentation** — harus lewat repository/usecase melalui provider/bloc.

## Handling Error & Log

- Pakai `debugPrint` atau logger terpusat, dilarang meninggalkan `print()` di production code.

## Catatan untuk AI Agent

- Jika task meminta sesuatu yang melanggar konvensi ini, konfirmasi dulu dan catat di `DECISIONS.md` jika disetujui untuk dilanggar.
- Aturan spesifik stack (misal: Moodle `upgrade.php` step) ada di `docs/stacks/*.md` — baca itu juga.
