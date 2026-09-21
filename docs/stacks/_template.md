# Stack Profile: [Nama Stack]

> Copy file ini jadi `docs/stacks/[nama].md` untuk stack baru (nextjs, laravel, dll).
> Bahasa: Indonesia. AI akan decide tipe stack jika belum ada profile-nya (AGENTS.md:7-8).

**Tipe:** `[frontend / backend / fullstack]` <!-- WAJIB isi, dipakai AI untuk manifest fallback -->
**Version:** [misal: Next.js 14]
**Package manager:** [npm / composer]

## Kebutuhan Dokumen (Manifest — WAJIB isi untuk selective copy)

Tentukan Wajib/Opsional/Tidak sesuai tipe:

| Kategori | File | Wajib? | Alasan |
|---|---|---|---|
| 00_overview | `ARCHITECTURE.md`, `STATE.md`, `STACK.md` | Ya | selalu |
| 03_logs | `PROGRESS_LOG.md`, `DECISIONS.md`, `CHANGELOG.md` | Ya | selalu |
| 01_guides | `GETTING_STARTED.md`, `CONVENTIONS.md`, `GLOSSARY.md` | Ya | onboarding |
| 01_guides | `WORKFLOW.md` | Opsional | tanya |
| 02_reference | `API_REFERENCE.md` | [Ya/Tidak] | |
| 02_reference | `API_STYLE.md` | [Ya/Opsional] | |
| 02_reference | `UI_STYLE.md` | [Opsional/Tidak] | hanya frontend |
| 02_reference | `DATABASE_SCHEMA.md` | [Ya/Tidak] | wajib untuk backend |
| 02_reference | `SECURITY_AND_DATA.md` | [Ya/Opsional/Tidak] | |
| modules | `modules/_template.md` | Ya | |

**Fallback untuk AI jika tipe tidak dikenal:**

- `frontend` (Next.js, Vue, React, Flutter) → ikut rule `flutter.md`: `API_*` Wajib, `UI_STYLE` Opsional, `DATABASE_SCHEMA` Tidak.
- `backend` (Laravel, Express, Moodle, Go) → ikut rule `moodle.md`: `DATABASE_SCHEMA` Wajib, `SECURITY_AND_DATA` Wajib, `UI_STYLE` Tidak.
- `fullstack` → semua `02_reference/*` Wajib.
- Jika ragu → **tanya user**: “Ini frontend atau backend? Mau saya buatkan DATABASE_SCHEMA.md juga?”

---

## Struktur Folder Wajib

```
[isi struktur folder yang benar untuk stack ini]
```

## Command Penting

| Perlu | Command |
|---|---|
| Install | |
| Run dev | |
| Test | |
| Build | |

## Library Wajib / Dilarang

| Library | Status | Alasan |
|---|---|---|
| | Wajib / Rekomendasi / Dilarang | |

## Konvensi Khusus Stack Ini

- [Aturan spesifik stack ini yang tidak ada di `01_guides/CONVENTIONS.md`]

## Checklist Sebelum Selesai

- [ ] [cek apa]
