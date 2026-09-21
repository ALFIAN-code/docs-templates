# Template Modul — Copy file ini untuk modul baru

> Cara pakai: copy file ini jadi `docs/modules/[nama-modul].md` jika modul sederhana, atau jadi `docs/modules/[nama-modul]/README.md` jika modul kompleks yang akan dipecah per fitur.
> Hapus blok instruksi `[...]` setelah diisi. Lihat `AGENTS.md:9` untuk aturan kapan pakai 1 file vs folder.
> Bahasa: Indonesia.

**Terakhir diupdate:** [YYYY-MM-DD]
**Status:** Planned / WIP / Done

## Overview Modul

[1-2 paragraf: modul ini ngapain, untuk siapa, kenapa dipisah jadi modul sendiri]

**Lokasi kode:** `src/modules/[nama]/` atau `lib/features/[nama]/` (sesuai stack)
**Dependencies:** [modul lain yang dipakai, misal: `auth`, `payment`]
**Dependents:** [modul lain yang memakai modul ini]

## Fitur

> Jika modul sederhana, tulis semua fitur di sini pakai `###`. Jika kompleks, cukup tulis daftar fitur + link ke file per fitur di `docs/modules/[nama]/[fitur].md`.

### Fitur 1: [Nama fitur, misal: Login]

- **Fungsi:** [apa yang dilakukan]
- **Lokasi:** `src/...`
- **Flow:**
  ```mermaid
  flowchart LR
    A[User Input] --> B[Validasi] --> C[API Call]
  ```
- **API terkait:** `POST /auth/login` (lihat `API_REFERENCE.md`)
- **Tabel terkait:** `users` (lihat `DATABASE_SCHEMA.md`)
- **Catatan khusus:** [edge case, workaround]

#### Sub-fitur 1.1: [Jika perlu grouping lagi]

[Detail sub-fitur. Pakai `####` untuk sub-grouping. Jangan buat folder baru untuk sub-fitur kecuali sangat kompleks.]

### Fitur 2: [Nama fitur berikutnya]

- **Fungsi:**
- **Lokasi:**
- **Flow:**
- **Catatan khusus:**

## State / Data Flow (jika relevan)

[Jelaskan state management khusus modul ini, misal: Riverpod provider untuk Flutter, atau session handling untuk Moodle. Jika tidak ada yang khusus, hapus bagian ini.]

## Konfigurasi & Env Khusus Modul

| Variable / Config | Fungsi | Wajib? |
|---|---|---|
| | | |

## Catatan Penting untuk AI Agent

- [Hal yang sering salah, misal: "jangan ubah field X karena dipakai modul Y"]
- [Konvensi khusus modul ini yang beda dari `CONVENTIONS.md` global, jika ada]

## Checklist Saat Ubah Modul Ini

- [ ] Update file ini (atau file fitur terkait) jika tambah/ubah fitur
- [ ] Update `ARCHITECTURE.md` tabel Daftar Modul jika modul baru
- [ ] Update `API_REFERENCE.md` jika ada endpoint baru
- [ ] Update `DATABASE_SCHEMA.md` jika ada tabel/kolom baru
- [ ] Tulis entry di `PROGRESS_LOG.md`
