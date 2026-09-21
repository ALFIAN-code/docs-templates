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

### 3. Jika Project Pakai Custom Library (Nedo UI & nedo_mobile_core)

- Project Flutter ini menggunakan **Nedo Design System & Core Library** (`nedo_mobile_core` / `packages/nedo-library`):
  - **Komponen Form & Tombol:** Gunakan `BpNedoButton`, `NedoIconButton`, `BpNedoTextField`, `BpNedoDatePicker`, `BpNedoBadge`.
  - **Ikon & Feedback:** Gunakan `NedoIcon`, `NedoIcons.*`, `NedoToast.success()`, `NedoToast.error()`, `NedoToast.info()`.
  - **Layout & Scaffold:** Gunakan `NdScaffold`, `NdAppBar`.
- Sebelum membuat widget UI baru, **cek dulu komponen Nedo dan shared widget** yang tersedia di:
  ```bash
  ls lib/modules/shared/presentation/widgets/
  ```
- Utamakan menggunakan atau memperluas widget dari `lib/modules/shared/presentation/widgets/` (seperti `SharedFileAttachmentCardWidget`, `SharedStudentMemberListCard`, `SharedSectionHeaderWidget`, `SharedProgressBarWidget`, `SharedTimelineWidget`).
- Jika library internal tidak tersedia langsung di workspace AI, tanyakan akses kepada developer alih-alih membuat duplikat komponen dari nol.

### 4. Standarisasi Kontainer Kartu — Wajib `t.cardDecoration`

- **Dilarang keras** membuat `BoxDecoration` manual untuk kartu (`color: Colors.white`, `boxShadow: [BoxShadow(...)]`).
- Setiap kartu / panel / kontainer section **wajib menggunakan extension `cardDecoration`** dari:
  ```dart
  import 'package:your_app/core/ui/theme/app_card_theme.dart';
  ```
- Format pemakaian:
  ```dart
  final t = NedoThemeData.of(context);

  Container(
    decoration: t.cardDecoration(radius: t.radius4xl), // atau t.cardDecoration() untuk default radius
    child: ...,
  )
  ```
- **Karakteristik `cardDecoration`:**
  - Menghasilkan efek *Ambient Glow* (dual-layer shadow: perimeter contact shadow halus + ambient brand glow yang menyebar lembut).
  - Otomatis adaptif Light Mode dan Dark Mode (`t.colorSurface` + `t.shadowSm`).
  - Untuk hero section bergradien gelap, tersedia `t.heroAmbientGlowShadow`.

### 5. Design Tokens & Theme Accessor (`NedoThemeData` / `t.*`)

- Seluruh styling warna, jarak, font, dan radius **wajib menggunakan token tema**:
  ```dart
  final t = NedoThemeData.of(context);
  ```
- **Aturan Token:**
  - **Warna:** `t.colorBrandBlue`, `t.colorSurfaceSubtle`, `t.colorText`, `t.colorTextSubtle`, `t.colorBorderSubtle`, `t.colorInfo`, `t.colorError`, `t.colorSuccess`.
  - **Spacing:** `t.spacingXs` (4), `t.spacingSm` (8), `t.spacingMd` (16), `t.spacingLg` (24), `t.spacingXl` (32).
  - **Radius:** `t.radiusSm`, `t.radiusMd`, `t.radiusLg`, `t.radiusXl`, `t.radius3xl`, `t.radius4xl`.
  - **Tipografi & Weight:** `t.fontSizeSm`, `t.fontWeightMedium`, `t.fontWeightBold`, dll.
- **Larangan Keras:** Dilarang meletakkan warna mentah seperti `Color(0xFF...)` atau `Colors.blue` langsung di widget. Semua wajib lewat token `t.*`.

### 6. Standarisasi Localization — Wajib `context.t(...)`

- **Dilarang keras menulis *hardcoded string* (teks mentah)** di widget UI.
- Semua teks UI (judul, subtitle, label form, placeholder, button, dialog, status toast) **wajib menggunakan helper localization**:
  ```dart
  context.t('ojt.form.coverLetter.title')
  context.t('ojt.home.nextActionTitle')
  ```
- **Jika key belum ada di dictionary:**
  - Daftarkan key baru secara rapi dan modular ke file lokalisasi bahasa (`l10n/` atau localization provider).
  - Ikuti hierarki penamaan: `[modul].[halaman_atau_fitur].[nama_elemen]`.

### 7. Konsistensi Page Shell — Wajib `NdScaffold`, `NdAppBar`, `NdAppBarButton`, & `BottomBar`

Hindari penggunaan widget shell dari `material.dart` langsung di modul. Gunakan arsitektur wrapper terstandarisasi:

- **Page Scaffold (`NdScaffold`):**
  - Semua halaman fitur/modul **wajib dibungkus dengan `NdScaffold`** dari:
    ```dart
    import 'package:your_app/modules/shared/presentation/widget/nedo_ui/nd_scaffold.dart';
    ```
  - **Dilarang menggunakan `Scaffold` bawaan `material.dart`** langsung di modul persona.
  - Parameter standar: `backgroundColor: t.colorSurfaceSubtle`, `appBar: NdAppBar(...)`, `body: ...`, `bottomBar: ...`.

- **Top Navigation (`NdAppBar`):**
  - **Wajib menggunakan `NdAppBar`** dari `lib/modules/shared/presentation/widget/nedo_ui/nd_app_bar.dart` (bukan `AppBar` bawaan Material).
  - Mendukung `title` terintegrasi dan `subtitle` opsional (misal nama perusahaan, periode semester, atau status):
    ```dart
    appBar: NdAppBar(
      title: context.t('ojt.form.coverLetter.title'),
      subtitle: context.t('ojt.form.coverLetter.subtitle'),
      actions: [ ... ],
    )
    ```
  - Tombol kembali (*back button*) otomatis aktif dengan styling rounded 44x44 dan border subtle yang seragam.

- **Tombol Aksi di AppBar (`NdAppBarButton`):**
  - Setiap tombol aksi pada `actions` di `NdAppBar` **wajib menggunakan `NdAppBarButton`**:
    ```dart
    NdAppBarButton(
      icon: NedoIcon(NedoIcons.document, size: 18, color: t.colorText),
      onPressed: _saveDraft,
    )
    ```
  - **Larangan:** Dilarang membuat kontainer kotak custom manual dengan border/radius sembarangan untuk tombol aksi di AppBar. Semua tombol leading dan actions harus proporsional (44x44, radius 14, background `colorSurface`, border `colorBorderSubtle`).

- **Sticky Footer & Action Bar (`SharedBottomActionBarWidget`):**
  - Untuk halaman form, detail, review, atau wizard yang memiliki tombol aksi di bagian bawah, **wajib menggunakan `SharedBottomActionBarWidget`** pada parameter `bottomBar` di `NdScaffold`:
    ```dart
    bottomBar: SharedBottomActionBarWidget(
      stat: const SizedBox.shrink(), // atau info status/teks ringkasan
      actions: [
        BpNedoButton(label: 'Simpan draf', variant: BpNedoButtonVariant.outline, color: BpNedoButtonColor.neutral, onPressed: _saveDraft),
        BpNedoButton(label: 'Ajukan', color: BpNedoButtonColor.primary, onPressed: _submit),
      ],
    )
    ```
  - Widget ini sudah adaptif terhadap keyboard inset, safe area bawah, dan *auto-stack* vertikal jika layar sempit.

### 8. Clean Code — Wajib

- Ikuti `01_guides/CONVENTIONS.md` + prinsip clean code:
  - 1 function / widget = 1 tanggung jawab, maksimal ~50 baris. Jika lebih, pecah jadi widget/function kecil.
  - Nama jelas (bukan `data1`, `tempWidget`), hindari magic number/string — pakai constant di `lib/core/constants/` atau `lib/modules/shared/`.
  - Jangan ada logic bisnis di `presentation/widgets/` — taruh di `domain/usecases` atau `data/repositories` → `provider/bloc`.
  - Struktur clean: `presentation` hanya UI + state, `domain` untuk entity/usecase, `data` untuk model/datasource. Jangan bypass layer.
  - Hapus `print`, `TODO` selesai, dan import tidak terpakai (akan ketangkep `flutter analyze`).
  - Beri komentar hanya untuk logic non-obvious (kenapa, bukan apa).

## Checklist Sebelum Selesai

- [ ] `flutter analyze` tanpa warning/error? (wajib, lihat Aturan 1)
- [ ] Page Shell & AppBar konsisten? (Wajib pakai `NdScaffold`, `NdAppBar`, dan `NdAppBarButton` di actions; bebas `Scaffold`/`AppBar` Material langsung)
- [ ] Sticky Bottom Bar menggunakan `SharedBottomActionBarWidget` untuk aksi bawah halaman?
- [ ] Card menggunakan `t.cardDecoration(...)` dari `app_card_theme.dart`? (Bebas `BoxDecoration` manual)
- [ ] Design Tokens dipatuhi via `t = NedoThemeData.of(context)`? (Bebas `Color(0xFF...)` mentah; pakai `t.color*`, `t.spacing*`, `t.radius*`)
- [ ] Localization dipatuhi via `context.t(...)`? (Bebas *hardcoded string* pada semua teks UI)
- [ ] UI pakai component Nedo (`BpNedo*`, `Nd*`) & reusable shared widgets? (Sudah cek `lib/modules/shared/presentation/widgets/` sebelum buat baru)
- [ ] Tidak ada duplikasi widget? (Variant baru via parameter `type`/`variant`, bukan copy-paste file baru)
- [ ] Clean Architecture layer dipatuhi? (`presentation` tidak ada logic bisnis, clean di leaf `data/domain/presentation`)
- [ ] `dart format` sudah?
- [ ] Jika model baru, `build_runner` sudah?
- [ ] `02_reference/API_STYLE.md` sudah diikuti (wrapper, pagination)?
