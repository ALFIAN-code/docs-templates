# UI Style Guide / Design System

> **WAJIB** untuk setiap project yang punya UI (Flutter/Web/Next.js). Tanpa file ini, design system dibangun ulang dari ingatan tiap sesi dan hasilnya tidak konsisten.
> Detail implementasi tiap component ada di `modules/design-system/`. File ini = **kontrak** (token + aturan), file itu = **isi** (component per component).
> Bahasa: Indonesia.

**Terakhir diupdate:** [YYYY-MM-DD]
**Stack:** [Flutter / Next.js / dll — lihat STACK.md]
**Status desain:** `🟡 Draft` <!-- 🟡 Draft / ✅ Ratified -->

> Konvensi status: `✅ Ratified` = disepakati, boleh dipakai | `🟡 Draft` = sedang dibahas | `❌ Not doing` = sengaja tidak

## Prinsip

[1 kalimat: misal "Minimalis, clean, fokus ke readability, bukan playful"]

## Design Tokens

> Sumber kebenaran tunggal. Flutter: taruh di `lib/core/theme/app_colors.dart`, `app_text_styles.dart`, `app_spacing.dart`. Jangan hardcode di widget.

### Warna

| Token | Nilai | Contoh pakai | Alasan |
|---|---|---|---|
| `colorPrimary` | `#1A73E8` | Button, link | [misal: kontras 4.8:1 vs putih — lolos AA] |
| `colorSecondary` | `#34A853` | Success, badge | |
| `colorError` | `#EA4335` | Validasi | |
| `colorBackground` | `#FFFFFF` / `#F8F9FA` | | |
| `colorTextPrimary` | `#202124` | | |
| `colorTextSecondary` | `#5F6368` | Caption, meta | |

### Spacing & Radius

| Token | Nilai | Pemakaian |
|---|---|---|
| `spacingXs/Sm/Md/Lg/Xl` | `4 / 8 / 16 / 24 / 32` | Semua padding & margin kelipatan 4 |
| `radiusSm/Md/Lg` | `4 / 8 / 16` | Input, Card, Dialog |

### Typography

| Token | Size | Weight | Line height | Pakai untuk |
|---|---|---|---|---|
| `textDisplay` | 32 | Bold | 1.2 | Judul halaman |
| `textHeading` | 20 | SemiBold | 1.3 | Section |
| `textBody` | 14 | Regular | 1.5 | Konten |
| `textCaption` | 12 | Regular | 1.4 | Hint, meta |

## Component Inventory

> **Lifecycle** = status component, wajib diisi. Mencegah AI membuat component baru padahal sudah ada, atau memakai component yang sudah deprecated.

| Component | File | Variant | Lifecycle | Catatan |
|---|---|---|---|---|
| Button | `lib/modules/shared/presentation/widgets/app_button.dart` | primary, secondary, ghost | `✅ Built` | Wajib pakai, jangan `ElevatedButton` mentah |
| Input | `app_text_field.dart` | default, error, disabled | `✅ Built` | |
| Card | `app_card.dart` | default, elevated | `✅ Built` | |
| Empty state | `empty_view.dart` | default | Planned | |
| [component lain] | | | Planned / `🔴 Deprecated` | [alasan kalau deprecated] |

## Variant Matrix (States)

> Setiap component interaktif wajib punya state ini. Yang tidak ada di tabel = belum didefinisikan, jangan karangan sendiri.

| Component | Default | Hover | Pressed | Disabled | Loading | Error |
|---|---|---|---|---|---|---|
| Button | ✅ | ✅ | ✅ | ✅ | Planned | — |
| Input | ✅ | ✅ | — | ✅ | — | ✅ |
| Card | ✅ | — | — | — | — | — |

## Accessibility (Wajib)

| Aturan | Nilai |
|---|---|
| Kontras teks | Minimal 4.5:1 (AA). Kalau tidak lolos, ganti tokennya, jangan diakalin |
| Tap target | Minimal 48×48dp |
| Semantik | Pakai `Semantics()` untuk IconButton & gambar informatif; wajib ada `tooltip` |
| Skala font | Jangan set tinggi font dengan `MediaQuery.textScaler` clamp tanpa alasan |

## Dark Mode

[misal: derive otomatis dari 1 sumber token via `ColorScheme.fromSeed` — belum-final, masukkan ke Open Threads]

## Icons & Assets

- Icons: [Material Icons / Lucide / Custom]
- Images: `assets/images/`, daftarkan di `pubspec.yaml` (Flutter) atau `public/` (Next.js)

## Responsive / Platform

- Breakpoint (web): `mobile <768, tablet <1024, desktop >=1024`
- Flutter: handle `MediaQuery`, jangan hardcode width 360.

## Open Threads (Belum Selesai)

> WAJIB dicek sebelum membuat token/component baru. Kalau sudah tertulis di sini, berarti masih dibahas — tanyakan, jangan karangan sendiri.

- [ ] [misal: skala tipografi — pakai Material 3 atau custom?]
- [ ] [misal: elevasi — pakai shadow atau border untuk memisahkan surface?]

## Catatan untuk AI Agent

- **Sebelum bikin component/token baru:** cek Component Inventory di atas + `ls lib/modules/shared/presentation/widgets/`. Kalau sudah ada tapi belum cukup → tambah **variant**, jangan buat file baru.
- **Jangan hardcode** warna/font/spacing/radius di widget — selalu lewat token di atas.
- **Butuh token baru?** usulkan di sini dulu (L1: tanya user), baru dipakai di kode.
- **Before finalize**, isi variant matrix + accessibility — component tanpa state yang jelas akan dipakai salah.