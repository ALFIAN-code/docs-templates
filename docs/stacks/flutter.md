# Stack Profile: Flutter — Frontend/Mobile

> Template stack untuk project Flutter. Saat init project Flutter, AI akan **merge isi file ini** ke `docs/00_overview/STACK.md` dan **hanya copy file yang Wajib** sesuai tabel di bawah (AGENTS.md:7).
> Bahasa: Indonesia.

**Tipe:** `frontend` (mobile)
**Flutter version:** [3.22.x, Dart 3.4.x]
**State management:** [Riverpod 2.x / Bloc — pilih 1]

## Kebutuhan Dokumen (Manifest — Dipakai AI untuk Selective Copy)

> AI WAJIB baca tabel ini saat init. Hanya copy yang `Wajib = Ya`. Yang `Opsional` → tanya dulu.

| Kategori | File | Wajib? | Alasan |
|---|---|---|---|
| 00_overview | `ARCHITECTURE.md`, `STATE.md`, `STACK.md` | Ya | inti, selalu ada |
| 03_logs | `PROGRESS_LOG.md`, `DECISIONS.md`, `CHANGELOG.md` | Ya | history |
| 01_guides | `GETTING_STARTED.md`, `CONVENTIONS.md`, `GLOSSARY.md` | Ya | onboarding |
| 01_guides | `WORKFLOW.md` | Opsional | tanya, tim kecil tidak perlu |
| 02_reference | `API_REFERENCE.md` | Ya | **fokus utama frontend**: daftar endpoint yang di-consume |
| 02_reference | `API_STYLE.md` | Ya | **wajib**: wrapper `success/data/meta`, pagination, error style |
| 02_reference | `UI_STYLE.md` | Opsional | tanya: “Butuh design system? Jika ya, buatkan.” |
| 02_reference | `DATABASE_SCHEMA.md` | Tidak | frontend tidak pegang DB langsung. Jika butuh (offline cache/Isar/Hive), tanya dulu |
| 02_reference | `SECURITY_AND_DATA.md` | Opsional | hanya jika ada SecureStorage/token handling sensitif |
| modules | `modules/_template.md` | Ya | template per fitur |
| modules | `modules/dashboard/` contoh | Tidak | jangan copy contoh dashboard ke project baru, mulai kosong |

**Ringkasan untuk AI:** Flutter = frontend → `02_reference` fokus ke `API_*` + `UI_STYLE`, bukan `DATABASE_SCHEMA`. Jangan buat file DB tanpa konfirmasi.

---

## Struktur Folder Wajib (Clean Architecture per Modul, istilah `modules` bukan `features`)

```
lib/
├── main.dart
├── core/               # theme, utils, constants — jangan taruh logic fitur di sini
├── modules/
│   ├── shared/         # widget & util reusable lintas modul
│   │   └── presentation/
│   │       └── widgets/  # ← lokasi widget shared (AppButton, AppCard, dll)
│   ├── auth/           # contoh modul
│   │   ├── data/         # datasources, models, repositories (impl)
│   │   ├── domain/       # entities, repositories (abstract), usecases
│   │   └── presentation/ # pages, widgets, providers/bloc
│   ├── dashboard/      # modul dengan grouping
│   │   ├── analytics/  # grouping di dalam modul
│   │   │   ├── data/
│   │   │   ├── domain/
│   │   │   └── presentation/
│   │   ├── manajemen_user/
│   │   │   ├── data/
│   │   │   ├── domain/
│   │   │   └── presentation/
│   │   └── shared/     # khusus dashboard jika ada shared internal
│   └── ...
└── l10n/               # string terjemahan, jangan hardcode di widget
```

**Aturan:** Istilah yang dipakai adalah `modules`, bukan `features`. Setiap modul bisa punya grouping lagi (misal `dashboard/analytics`), clean layer `data / domain / presentation` ada di **ujung tree** (leaf), bukan di root. Cek `docs/00_overview/STACK.md` jika ada custom path.

**Larangan:** Jangan buat `lib/src/` atau `lib/features/` — pakai `lib/modules/`. Jangan call API langsung di `presentation/widgets/` — harus lewat `data/repositories/` via usecase.

## Command Penting

| Perlu | Command |
|---|---|
| Install | `flutter pub get` |
| Run dev | `flutter run --flavor dev` |
| Test | `flutter test` |
| Analyze | `flutter analyze` |
| Format | `dart format .` |
| Build APK | `flutter build apk --flavor prod` |
| Generate | `dart run build_runner build --delete-conflicting-outputs` |

## Library Wajib / Dilarang

| Library | Status | Alasan |
|---|---|---|
| `riverpod` / `flutter_bloc` | Wajib (pilih 1) | state management |
| `dio` atau `http` | Wajib | HTTP client |
| `freezed` + `json_serializable` | Rekomendasi | model |
| `get` (GetX) | Tanya dulu | konflik Riverpod/Bloc → butuh ADR |

Tambah library → catat di `03_logs/DECISIONS.md`.

## Konvensi Khusus Flutter

- File widget: `snake_case.dart`, class `PascalCase`
- Provider/Bloc: 1 file 1 provider, `*_provider.dart`
- Jangan `print()` → pakai `logger` / `debugPrint`
- Flavor `dev/staging/prod` — jangan hardcode base URL, pakai `--dart-define` / `env.dart`
- Asset di `assets/images/`, daftar di `pubspec.yaml`

## Build Runner

Jika ubah model `freezed`/`json_serializable`, wajib `build_runner` dan commit `.g.dart`.

## Aturan Wajib Flutter (Tambahan)

### 1. Selalu `flutter analyze` Setiap Selesai Fitur

- Setelah develop / ubah fitur apa pun, **wajib jalankan `flutter analyze`** sebelum klaim selesai.
- Jika ada warning/error → perbaiki dulu, jangan lanjut task lain.
- Catat hasilnya di `03_logs/PROGRESS_LOG.md` (“analyze: 0 issue” atau list yang diperbaiki).
- Ini bagian dari checklist di bawah — task dianggap belum selesai kalau belum analyze.

### 2. Develop UI Pakai Style Component & Reusable (Anti Duplikasi)

- Semua UI **wajib pakai component reusable** dari `lib/modules/shared/presentation/widgets/` atau dari `02_reference/UI_STYLE.md` + `00_overview/STACK.md` (design token).
- Sebelum buat widget baru, **cek dulu component yang tersedia**:
  ```bash
  ls lib/modules/shared/presentation/widgets/
  ```
- Jika component sudah ada tapi belum sesuai mockup → **jangan duplikasi jadi widget baru**. Kustomisasi via:
  - `type` / `variant` param → misal `AppButton(type: AppButtonType.primary)`
  - atau tambah parameter opsional → `AppCard(elevation, padding, hasShadow)`
  - **Pastikan tidak merusak pemakaian di halaman lain** — cek `grep -r AppButton lib/modules/` sebelum ubah signature.
- Jika butuh variant baru, update `02_reference/UI_STYLE.md` sekalian (L1: tanya dulu).
- Larangan: jangan hardcode warna/font/radius di widget — harus lewat token. Jangan copy-paste 1 widget jadi 2 file hanya karena beda padding. Cek `lib/modules/shared/presentation/widgets/` dulu.

### 3. Jika Project Pakai Custom Library

- Banyak project Flutter kamu pakai **custom library internal** (misal `packages/custom_lib/` atau package lokal di `pubspec.yaml` dengan `path:` / `git:`).
- Sebelum develop, **cek dulu tools & UI component di library tersebut**:
  ```bash
  ls packages/custom_lib/lib/src/widgets/ 2>/dev/null || ls lib/custom_lib/ 2>/dev/null
  cat pubspec.yaml | grep -A 5 custom
  ```
- Utamakan pakai widget/util dari custom library daripada buat dari nol.
- Jika project custom library **tidak tersedia di workspace AI** (tidak ada folder/file-nya), **jangan asumsi**. Tanya developer:
  > “Project custom library tidak ditemukan di workspace. Bisa tunjukkan path-nya atau izinkan saya akses? Saya tidak akan buat duplikat component sebelum konfirmasi.”
- Jika diizinkan, baca `00_overview/STACK.md` bagian custom library untuk lokasi yang benar dan catat di `03_logs/DECISIONS.md` jika ada keputusan pakai/tidak pakai library tersebut.

### 4. Clean Code — Wajib

- Ikuti `01_guides/CONVENTIONS.md` + prinsip clean code:
  - 1 function / widget = 1 tanggung jawab, maksimal ~50 baris. Jika lebih, pecah jadi widget/function kecil.
  - Nama jelas (bukan `data1`, `tempWidget`), hindari magic number/string — pakai constant di `lib/core/constants/` atau `lib/modules/shared/`.
  - Jangan ada logic bisnis di `presentation/widgets/` — taruh di `domain/usecases` atau `data/repositories` → `provider/bloc`.
  - Struktur clean: `presentation` hanya UI + state, `domain` untuk entity/usecase, `data` untuk model/datasource. Jangan bypass layer.
  - Hapus `print`, `TODO` selesai, dan import tidak terpakai (akan ketangkep `flutter analyze`).
  - Beri komentar hanya untuk logic non-obvious (kenapa, bukan apa).

## Checklist Sebelum Selesai

- [ ] `flutter analyze` tanpa warning/error? (wajib, lihat Aturan 1)
- [ ] UI pakai component reusable & sudah cek `lib/modules/shared/presentation/widgets/` + custom_lib? (Aturan 2 & 3)
- [ ] Tidak ada duplikasi widget & sudah pakai token dari `02_reference/UI_STYLE.md`? Variant baru pakai `type`/param, tidak duplikasi file?
- [ ] Clean Architecture layer dipatuhi? (`presentation` tidak ada logic bisnis, clean di leaf `data/domain/presentation`)
- [ ] `dart format` sudah?
- [ ] Jika model baru, `build_runner` sudah?
- [ ] `02_reference/API_STYLE.md` sudah diikuti (wrapper, pagination)?
