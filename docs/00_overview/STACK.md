# Stack Aktif

> File ini adalah **hasil merge** dari 1 stack yang terpilih dari template `docs/stacks/*.md`.
> Saat init, AI hanya ambil 1 stack (flutter/moodle/dll) dan merge ke sini. Folder `stacks/` tidak ikut ke project.
> Untuk ganti stack, edit file ini atau minta AI re-init dengan stack lain.

**Stack:** `flutter` <!-- ganti: flutter / moodle / nextjs / custom -->
**Tipe:** `frontend` <!-- frontend / backend / fullstack — tentukan untuk kebutuhan dokumen (lihat AGENTS.md:7) -->
**Versi:** [misal: Flutter 3.22, Dart 3.4]

**Alasan pilih stack ini:** [Isi kenapa pilih, misal: “Aplikasi mobile Flutter consume API backend Moodle”]

**Stack tambahan (jika ada, misal fullstack):**
- [misal: `moodle` untuk backend — tulis di sini dan merge aturannya di bawah]

---

## Aturan Stack Terpilih

> Tempelkan isi dari `agent-docs-template-v3/docs/stacks/[nama].md` ke bawah sini saat init.
> Contoh untuk Flutter, copy seluruh isi `stacks/flutter.md` mulai dari “Struktur Folder Wajib” ke bawah.
> Jangan lupa hapus placeholder `[...]` dan isi sesuai project.

[Placeholder — saat init Flutter, ganti blok ini dengan isi `stacks/flutter.md`]

---

## Kebutuhan Dokumen untuk Stack Ini

> Tabel ini dipakai AI untuk decide file mana yang di-copy saat init (AGENTS.md:7). Biarkan di sini sebagai jejak.

| Kategori | File | Wajib? |
|---|---|---|
| 00_overview | ARCHITECTURE.md, STATE.md, STACK.md | Ya |
| 01_guides | GETTING_STARTED, CONVENTIONS, GLOSSARY | Ya |
| 01_guides | WORKFLOW.md | Opsional |
| 02_reference | API_REFERENCE.md | Ya |
| 02_reference | API_STYLE.md | Ya (frontend) / Ya (backend, style beda) |
| 02_reference | UI_STYLE.md | Opsional (hanya frontend) |
| 02_reference | DATABASE_SCHEMA.md | Tidak (frontend) / Ya (backend) |
| 02_reference | SECURITY_AND_DATA.md | Opsional (frontend) / Ya (backend) |
| 03_logs | PROGRESS_LOG, DECISIONS, CHANGELOG | Ya |
| modules | modules/_template.md | Ya |
