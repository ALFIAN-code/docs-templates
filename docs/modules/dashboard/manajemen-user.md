# Fitur: Dashboard > Manajemen User

**Induk modul:** [Dashboard](./README.md)
**Terakhir diupdate:** [YYYY-MM-DD]
**Lokasi kode:** `lib/features/dashboard/users/` atau `src/modules/dashboard/users/`
**API terkait:** `GET /users`, `POST /users`, `PATCH /users/:id`

## Fungsi

CRUD user dari dalam dashboard (hanya role admin). Contoh fitur level 2 di dalam modul dashboard.

## Flow

- List user dengan pagination + search
- Tambah user → validasi email unik → `POST /users`
- Edit user → `PATCH /users/:id`

## Catatan untuk AI Agent

- Validasi email: cek `GLOSSARY.md` definisi `user` vs `member`.
- Jangan hardcode role, ambil dari `auth` modul.
