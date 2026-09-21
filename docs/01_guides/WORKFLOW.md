# Workflow Pengembangan

> Alur kerja Git, code review, dan rilis. Opsional — tim kecil bisa gabung dengan CONVENTIONS.md.

**Terakhir diupdate:** [YYYY-MM-DD]

## Branching

- Main: `main` (prod), `develop` (staging)
- Fitur: `feat/nama-fitur`, fix: `fix/nama-bug`
- Jangan push langsung ke `main` — harus via PR.

## Code Review

- PR minimal 1 approver.
- CI harus hijau: `lint` + `test`.

## Rilis

1. Merge ke `develop` → staging
2. QA → tag `vX.Y.Z` → merge ke `main` → prod
3. Update `03_logs/CHANGELOG.md` saat tag.

## Catatan untuk AI Agent

- Jika AI diminta “langsung push ke main” → konfirmasi dulu (L1).
- Tulis ringkasan PR dalam bahasa Indonesia, kode tetap Inggris.
