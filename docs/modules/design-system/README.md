# Design System

> Detail implementasi design system. **`02_reference/UI_STYLE.md` = kontrak** (token, aturan, matriks state). **File ini = isi** (component per component).
> Kalau butuh bikin component baru: cek dulu Component Inventory di `UI_STYLE.md` dan `ls lib/modules/shared/presentation/widgets/`.

**Terakhir diupdate:** [YYYY-MM-DD]
**Status:** Planned / WIP / Done
**Lokasi kode:** `lib/modules/shared/presentation/widgets/`

## Prinsip Design

[1-2 kalimat: apa yang membuat UI project ini terasa "kita", bukan generic.]

## Token

> Kontrak token ada di `02_reference/UI_STYLE.md`. Di sini cukup pointer ke file implementasinya.

| Kategori | File implementasi |
|---|---|
| Warna | `lib/core/theme/app_colors.dart` |
| Tipografi | `lib/core/theme/app_text_styles.dart` |
| Spacing & Radius | `lib/core/theme/app_spacing.dart` |
| Theme assembly | `lib/core/theme/app_theme.dart` |

## Component

> Tambahkan baris baru **di turn yang sama** saat component selesai dibahas. Satu sub-bagian
> per component. Lifecycle: `Planned` → `🔨 WIP` → `✅ Done` → `🔴 Deprecated`.

### [Nama Component] — `Planned`

- **File:** `lib/modules/shared/presentation/widgets/app_[nama].dart`
- **Varian:** [misal: primary, secondary, ghost]
- **State:** [default, hover, pressed, disabled, loading, error — yang mana yang sudah ada]
- **API utama:**
  ```dart
  AppButton({ required String label, required VoidCallback? onPressed, AppButtonType type = AppButtonType.primary, bool isLoading = false })
  ```
- **Screenshot/usage:** [link atau contoh pemakaian singkat]
- **Catatan:** [kenapa params ini dipilih — misal: "pakai `type`, bukan `color`, supaya caller tidak bisa sembarang pilih warna"]

### [Component Berikutnya] — `Planned`

- **File:**
- **Varian:**
- **State:**
- **Catatan:**

## Composite Pattern

> Kalau ada pola yang berulang dari beberapa component (misal form field + label + error
> selalu sama), tulis di sini sebagai aturan reusable — jangan ulang di tiap component.

- [misal: "Semua form wajib pakai `FormFieldRow` — jangan susun Label+Input+Error manual"]

## Open Threads (Belum Selesai)

> **AI WAJIB cek sebelum bikin component/token baru.** Kalau sudah tertulis di sini berarti
> masih dibahas — tanyakan, jangan putuskan sendiri.

- [ ] [misal: apakah perlu `AppModal` generik atau pakai `showDialog` bawaan?]
- [ ] [misal: animasi transisi — boleh pakai animasi default Material atau custom?]

## Checklist Saat Tambah Component

- [ ] Sudah cek `UI_STYLE.md` Component Inventory — memang belum ada? (bukan cuma perlu variant beda)
- [ ] Sudah `grep -r "NamaComponent" lib/` — tidak akan merusak pemakaian lain?
- [ ] Token dipakai, tidak ada warna/spacing hardcode?
- [ ] State di Variant Matrix terisi semua
- [ ] Dipakai minimal di 2 halaman sebelum dianggap `✅ Done`
- [ ] Tambah baris di Component Inventory (`UI_STYLE.md`)
- [ ] Entry `PROGRESS_LOG.md` ditulis

## Catatan Penting untuk AI Agent

- Component tanpa state (disabled/loading/error) yang jelas akan dipakai salah → isi dulu
  matriksnya, baru dipakai.
- Kalau butuh variant baru dari component yang sudah ada → tambah **variant**, jangan buat file baru.
- Kalau component di-*deprecated*, jangan hapus langsung — tandai `🔴 Deprecated` dulu, catat
  alasannya di sini, baru migrate pemakaiannya.