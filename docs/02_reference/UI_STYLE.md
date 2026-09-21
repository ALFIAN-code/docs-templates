# UI Style Guide / Design System

> Style UI untuk frontend. Opsional — hanya buat jika project frontend (Flutter/Web) butuh konsistensi desain. Untuk backend murni, file ini tidak perlu.
> Bahasa: Indonesia.

**Terakhir diupdate:** [YYYY-MM-DD]
**Stack:** [Flutter / Next.js / dll — lihat STACK.md]

## Prinsip

[1 kalimat: misal “Minimalis, clean, fokus ke readability, bukan playful”]

## Design Tokens

| Token | Nilai | Contoh pakai |
|---|---|---|
| Primary | `#1A73E8` | Button, link |
| Secondary | `#34A853` | Success, badge |
| Error | `#EA4335` | Validasi |
| Background | `#FFFFFF` / `#F8F9FA` | |
| Text | `#202124` | |
| Radius | `8px` | Card, button |
| Spacing | `4, 8, 16, 24` | Padding/margin kelipatan 8 |

> Untuk Flutter: taruh di `lib/core/theme/app_colors.dart` dan `app_text_styles.dart`, jangan hardcode di widget.

## Typography

| Style | Size | Weight | Pakai untuk |
|---|---|---|---|
| Display | 32 | Bold | Judul halaman |
| Heading | 20 | SemiBold | Section |
| Body | 14 | Regular | Konten |
| Caption | 12 | Regular | Hint, meta |

## Components

| Component | Library / File | Catatan |
|---|---|---|
| Button | `lib/core/widgets/app_button.dart` | Primary, secondary, ghost |
| Input | `app_text_field.dart` | Wajib pakai, jangan `TextField` mentah |
| Card | `app_card.dart` | Radius 8, shadow light |
| Empty state | `empty_view.dart` | |

**Larangan:** Jangan pakai warna/font langsung di widget — harus lewat token di atas.

## Icons & Assets

- Icons: [Material Icons / Lucide / Custom]
- Images: `assets/images/`, daftarkan di `pubspec.yaml` (Flutter) atau `public/` (Next.js)

## Responsive / Platform

- Breakpoint (web): `mobile <768, tablet <1024, desktop >=1024`
- Flutter: handle `MediaQuery`, jangan hardcode width 360.

## Catatan untuk AI Agent

- Sebelum buat widget baru, cek `00_overview/STACK.md` dan file ini — pakai token & component yang sudah ada.
- Jika butuh warna/component baru, usulkan update ke file ini dulu (L1: tanya), jangan langsung hardcode.
