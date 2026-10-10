# Arsitektur Sistem

**Terakhir diupdate:** [YYYY-MM-DD]
**Stack aktif:** lihat `STACK.md` di folder yang sama

## Status Keseluruhan

**Fase desain:** `🟡 Draft` <!-- 🟡 Draft (masih dibahas) / ✅ Ratified (sudah disepakati) -->
**Arti status ini:** kalau masih `🟡 Draft`, berarti belum ada yang dikunci — jangan bangun implementasi berat di atasnya. Kalau `✅ Ratified`, semua keputusan di bawah boleh dipakai tanpa tanya lagi.

> Konvensi status dipakai konsisten di seluruh `docs/`:
> `✅ Ratified` = disepakati, boleh dipakai | `🟡 Draft` = sedang dibahas, jangan diasumsikan final | `❌ Not doing` = sengaja tidak, jangan usulkan ulang

## Overview

[Deskripsi singkat: aplikasi ini apa, untuk siapa, masalah apa yang diselesaikan. 3-5 kalimat. Detail ringkas ada di `STATE.md`.]

## Non-Goals (Yang Sengaja Tidak Dibuat)

> Mencegah AI dan developer mengusulkan fitur yang di luar scope. Isi dengan batasan yang sudah disepakati.

- [misal: tidak ada mode offline di v1]
- [misal: tidak support web di v1, mobile only]
- [misal: tidak ada role selain admin & user]

## Tech Stack

| Layer | Teknologi | Alasan |
|---|---|---|
| Frontend | | |
| Backend | | |
| Database | | |
| Auth | | |
| Hosting/Infra | | |
| Queue/Cache | | |

> Aturan spesifik per stack ada di `STACK.md` (hasil merge dari `stacks/*.md` template). Jangan duplikasi di sini.

## Keputusan Arsitektur (Ringkasan)

> Ringkasan keputusan lintas-modul. Alasan lengkap + alternatif yang ditolak ada di `03_logs/DECISIONS.md`.
> Kolom status wajib diisi — ini yang membedakan "sudah diputuskan" dari "lagi dibahas".

| Keputusan | Status | Alasan Singkat | ADR |
|---|---|---|---|
| [misal: Riverpod, bukan Bloc] | `🟡 Draft` | [testable tanpa provider mock] | ADR-001 |
| [misal: token warna dari 1 sumber] | `✅ Ratified` | [konsistensi dark mode] | ADR-002 |

## Struktur Folder

```
project/
├── lib/ atau src/              # lihat STACK.md untuk detail
│   ├── features/ atau modules/
├── docs/
│   ├── 00_overview/            # kamu di sini
│   │   ├── ARCHITECTURE.md     # index ini
│   │   ├── STATE.md
│   │   └── STACK.md
│   ├── 01_guides/
│   ├── 02_reference/
│   ├── 03_logs/
│   └── modules/                # detail per modul
└── ...
```

## Alur Data / Flow Utama

```mermaid
flowchart LR
  Client[Client/Browser] --> API[API Server]
  API --> DB[(Database)]
  API --> Ext[External Service]
```

[Flow request paling umum. Untuk flow per modul, taruh di `modules/[modul].md`.]

## Daftar Modul

> **Aturan modular (`AGENTS.md:9`):** File ini hanya index. Detail tiap modul ada di `docs/modules/`. AI wajib baca file modul yang relevan sebelum kerjakan task di modul tersebut.

| Modul | Deskripsi singkat | Dokumen | Status |
|---|---|---|---|
| [Auth] | Login, register, role | [modules/auth.md](../../docs/modules/auth.md) | Done / WIP |
| [Dashboard] | Analitik, manajemen user | [modules/dashboard/](../../docs/modules/dashboard/) | WIP |
| [Pembayaran] | Checkout, invoice | [modules/pembayaran.md](../../docs/modules/pembayaran.md) | Planned |
| [Design System] | Token, component reusable | [modules/design-system/](../../docs/modules/design-system/) | WIP |

*Jika modul sederhana (<200 baris, 1-3 fitur): 1 file `modules/nama.md`.*
*Jika kompleks (>3 fitur): folder `modules/nama/README.md` + file per fitur.*

## Integrasi Eksternal

| Service | Fungsi | Auth | Docs |
|---|---|---|---|
| | | | |

## Environment Variables Penting

| Variable | Fungsi | Wajib? |
|---|---|---|
| | | |

> Cara setup env ada di `01_guides/GETTING_STARTED.md`.

## Open Threads (Diskusi Belum Selesai)

> **AI WAJIB cek bagian ini sebelum mengusulkan pendekatan.** Kalau sudah tertulis di sini berarti justru sedang dibahas dan belum diputuskan — tanyakan, jangan usulkan seolah baru kepikiran.
> Item yang sudah diputuskan **pindah ke** tabel "Keputusan Arsitektur" di atas (hapus dari sini).

- [ ] [misal: pagination — infinite scroll atau cursor-based? (kebanyakan InfiniteScroll, belum diputuskan)]
- [ ] [misal: dark theme — derive dari satu sumber atau regenerate manual?]

## Catatan Penting untuk AI / Dev Baru

- [Hal non-obvious, misal: “field `status` pakai integer bukan enum karena X”]
- [Workaround yang sengaja dipertahankan]
- [Link ke `01_guides/GLOSSARY.md` jika ada istilah yang perlu disepakati]