# Dokumentasi Project

Folder `docs/` adalah **single source of truth** untuk manusia & AI. Karena AI tidak punya ingatan antar sesi, folder ini adalah “memori eksternal” project.

> **Untuk AI:** Baca `AGENTS.md` di root project dulu untuk urutan baca lengkap. File ini hanya peta navigasi.

## Peta — 4 Kategori + Modules

```
docs/
├── README.md              ← kamu di sini (peta)
├── 00_overview/           ★ dibaca tiap sesi
├── 01_guides/             ○ dibaca saat onboarding
├── 02_reference/          ◇ dibaca saat butuh detail teknis
├── 03_logs/               ● history append-only
└── modules/               ◆ detail fitur per modul
```

| Kategori | Isi | Kapan dibuka | Untuk siapa |
|---|---|---|---|
| **`00_overview/`** | `ARCHITECTURE.md` (index), `STATE.md` (ringkasan 1 hal), `STACK.md` (aturan stack terpilih) | Tiap sesi, selalu | Manusia + AI |
| **`01_guides/`** | `GETTING_STARTED.md`, `CONVENTIONS.md`, `GLOSSARY.md`, `WORKFLOW.md` | Onboarding / mau tau aturan nulis | Manusia, AI saat awal |
| **`02_reference/`** | `API_REFERENCE.md`, `API_STYLE.md`, `UI_STYLE.md`, `DATABASE_SCHEMA.md`, `SECURITY_AND_DATA.md` | Saat bikin/consume API, DB, UI | Dev + AI saat coding |
| **`03_logs/`** | `PROGRESS_LOG.md`, `DECISIONS.md`, `CHANGELOG.md` | Tiap sesi & saat cari histori keputusan | AI wajib, manusia saat review |
| **`modules/`** | `modules/[nama]/README.md` + `[fitur].md` | Saat kerjakan fitur di modul itu | Dev + AI |

## Cara Pakai untuk Manusia

1. **Baru clone?** → `01_guides/GETTING_STARTED.md` → `01_guides/CONVENTIONS.md`.
2. **Mau paham sistem?** → `00_overview/ARCHITECTURE.md` → `00_overview/STATE.md`.
3. **Mau tambah fitur?** → cari `modules/[namamodul]/` → baca `README.md` modul itu.
4. **Mau hit API?** → `02_reference/API_STYLE.md` dulu (kontrak), baru `API_REFERENCE.md`.

## Cara Pakai untuk AI

Lihat `AGENTS.md:1` di root — urutan baca: `03_logs/PROGRESS_LOG.md` → `00_overview/STATE.md` → `00_overview/ARCHITECTURE.md` → `00_overview/STACK.md` → `02_reference/API_STYLE.md` (jika frontend) → dst.

**Penting (L1):** Template v3 punya banyak file, tapi **tidak semua di-copy ke project**. AI hanya copy yang `Wajib` untuk stack terpilih (lihat `stacks/*.md` di template bagian Kebutuhan Dokumen). Lihat `AGENTS.md:7`.

## Aturan Singkat

- **Append, jangan overwrite** untuk `03_logs/*`.
- **Singkat & akurat** > panjang tapi basi.
- `00_overview/ARCHITECTURE.md` adalah index — detail di `modules/`. Jika modul >200 baris, pecah jadi `modules/[nama]/README.md` + file per fitur.
- Bahasa docs: Indonesia. Kode: Inggris.
