# UI Style Guide / Design System

> Style UI untuk frontend. Opsional — hanya buat jika project frontend (Flutter/Web) butuh konsistensi desain. Untuk backend murni, file ini tidak perlu.
> Bahasa: Indonesia.

**Terakhir diupdate:** [YYYY-MM-DD]
**Stack:** [Flutter / Next.js / dll — lihat STACK.md]

## Prinsip

[1 kalimat: misal “Minimalis, clean, fokus ke readability, bukan playful”]

## Design Tokens (Nedo Theme Tokens)

Untuk project Flutter dengan Nedo Design System, seluruh styling wajib menggunakan accessor:
```dart
final t = NedoThemeData.of(context);
```

| Kategori Token | Akses via `t.*` | Kegunaan |
|---|---|---|
| **Primary/Brand** | `t.colorPrimary`, `t.colorBrandBlue` | Tombol utama, active state, indicator |
| **State/Semantic** | `t.colorSuccess`, `t.colorWarning`, `t.colorError`, `t.colorInfo` | Badge status, alert, validasi |
| **Surface/Background** | `t.colorSurface`, `t.colorSurfaceSubtle` | Latar belakang halaman & card |
| **Text** | `t.colorText`, `t.colorTextSubtle`, `t.colorTextDisabled` | Hirarki keterbacaan teks |
| **Border** | `t.colorBorder`, `t.colorBorderSubtle` | Divider dan outline |
| **Spacing** | `t.spacingXs` (4), `t.spacingSm` (8), `t.spacingMd` (16), `t.spacingLg` (24), `t.spacingXl` (32) | Padding dan margin |
| **Radius** | `t.radiusSm` (4), `t.radiusMd` (8), `t.radiusLg` (12), `t.radiusXl` (14), `t.radius3xl` (16), `t.radius4xl` (18-20) | Sudut melengkung card dan tombol |

**Larangan:** Dilarang menggunakan warna mentah (`Color(0xFF...)` atau `Colors.blue`) langsung di widget — wajib menggunakan token `t.*`.

## Kontainer Kartu — `t.cardDecoration` (Ambient Glow)

Setiap kontainer card atau panel section **wajib menggunakan extension `cardDecoration`** dari `core/ui/theme/app_card_theme.dart`:

```dart
Container(
  decoration: t.cardDecoration(radius: t.radius4xl), // atau t.cardDecoration()
  child: ...,
)
```
- **Karakteristik:** Menghasilkan efek *Ambient Glow* (dual-layer shadow lembut tanpa garis kaku), adaptif otomatis pada Light Mode dan Dark Mode.
- **Hero Card:** Gunakan `t.heroAmbientGlowShadow` untuk hero card bergradien biru pekat.

## Typography

Gunakan ukuran dan bobot font terstandarisasi dari `t`:
- Display / Page Title: `t.fontSize2xl` / `t.fontWeightBold`
- Section Title: `t.fontSizeMd` (14-16) / `t.fontWeightBold`
- Body Text: `t.fontSizeSm` (12-14) / `t.fontWeightRegular`
- Caption / Meta / Badge: 10-11 / `t.fontWeightMedium` atau `t.fontWeightSemiBold`

## Components (Nedo UI & Shared)

| Jenis Komponen | Komponen Resmi | Contoh / Catatan |
|---|---|---|
| **Page Shell** | `NdScaffold` | Wrapper halaman wajib (bukan `Scaffold` Material). Properti: `appBar`, `body`, `bottomBar` |
| **Top Navigation** | `NdAppBar`, `NdAppBarButton` | AppBar dengan title, subtitle, back button otomatis, dan actions via `NdAppBarButton` (44x44, radius 14) |
| **Sticky Bottom Bar** | `SharedBottomActionBarWidget` | Footer bar di `NdScaffold.bottomBar` untuk slot status + tombol aksi bawah |
| **Button** | `BpNedoButton`, `NedoIconButton` | Variant: `solid`, `outline`, `soft`. Color: `primary`, `neutral`, `destructive` |
| **Form Input** | `BpNedoTextField`, `BpNedoDatePicker` | Wajib pakai, mendukung label, mandatory, & validator |
| **Badge** | `BpNedoBadge` | Variant: `success`, `warning`, `destructive`, `info`. Style: `soft` |
| **Feedback** | `NedoToast` | `NedoToast.success()`, `NedoToast.error()`, `NedoToast.info()` |
| **Icon** | `NedoIcon`, `NedoIcons.*` | Standard icon set dari library |
| **Shared Widgets** | `lib/modules/shared/presentation/widgets/` | `SharedFileAttachmentCardWidget`, `SharedStudentMemberListCard`, dll |

## Icons & Assets

- Icons: `NedoIcon(NedoIcons.[nama_ikon], size: 16-18, color: t.colorText)`
- Images: `assets/images/`, daftarkan di `pubspec.yaml`

## Catatan untuk AI Agent

- Selalu gunakan `final t = NedoThemeData.of(context);`.
- Semua halaman wajib dibungkus `NdScaffold` + `NdAppBar` (dilarang pakai `Scaffold`/`AppBar` Material langsung).
- Tombol aksi di AppBar wajib menggunakan `NdAppBarButton` (seragam dengan tombol back).
- Tombol aksi di bawah halaman wajib menggunakan `SharedBottomActionBarWidget`.
- Semua card wajib menggunakan `t.cardDecoration(...)`.
- Semua teks UI wajib dibungkus `context.t('key.path')` (lokalisasi).
- Sebelum membuat widget baru, cek `lib/modules/shared/presentation/widgets/` terlebih dahulu untuk menghindari duplikasi.
