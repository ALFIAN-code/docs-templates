# API Style Guide

> Kontrak style API yang dipakai project ini. Wajib dibaca sebelum pakai/tambah endpoint. Beda stack beda isi — lihat `00_overview/STACK.md` untuk tau style mana yang aktif.
> Bahasa: Indonesia.

**Terakhir diupdate:** [YYYY-MM-DD]
**Tipe stack:** [frontend/backend/fullstack — lihat STACK.md]

## Base URL & Versioning

| Env | Base URL | Contoh |
|---|---|---|
| Dev | `http://localhost:3000/api/v1` | |
| Prod | `https://api.example.com/v1` | |

Version di URL (`/v1`), bukan header. Breaking change → naik major.

## Format Response Wrapper (Frontend Wajib Ikut Ini)

Semua response pakai wrapper konsisten:

```json
{
  "success": true,
  "data": { },
  "message": "OK",
  "meta": { "page": 1, "limit": 20, "total": 100 }
}
```

- `success: false` → `data` null, `message` berisi error user-friendly, plus `errors` jika validasi.
- Jangan return array langsung di root — selalu bungkus `data`.

## Pagination

Query: `?page=1&limit=20&sort=created_at:desc`

Response `meta` wajib ada jika endpoint return list.

## Filter & Search

- Filter: `?status=active&from=2026-01-01&to=2026-01-31`
- Search: `?q=keyword`
- Format tanggal: `YYYY-MM-DD` (lihat `01_guides/CONVENTIONS.md`)

## Error Format

```json
{
  "success": false,
  "message": "Validasi gagal",
  "errors": { "email": ["Email sudah dipakai"] }
}
```

| Status | Arti | Aksi frontend |
|---|---|---|
| 400 | Bad request / validasi | Tampilkan `errors` per field |
| 401 | Unauthorized | Redirect login, refresh token |
| 403 | Forbidden | Tampilkan “tidak punya akses” |
| 404 | Not found | |
| 422 | Validasi (khusus Laravel) | Sama dengan 400 |
| 500 | Server error | Tampilkan generic + log |

## Auth

- Header: `Authorization: Bearer <token>`
- Refresh: `POST /auth/refresh` dengan `refresh_token`
- Untuk Moodle: pakai `wstoken` + `wsfunction`, lihat `STACK.md` (backend style).

## Naming Endpoint

- Plural noun: `/users`, `/users/:id/orders`
- Jangan pakai verb di URL: `POST /users` bukan `POST /createUser`
- Query param `snake_case`, body `camelCase` atau `snake_case` — konsisten (tulis di sini yang dipakai project).

## Contoh Request/Response

### `GET /users?page=1&limit=20`

Request header:
```
Authorization: Bearer xxx
```

Response 200:
```json
{
  "success": true,
  "data": [{ "id": "uuid", "name": "Budi" }],
  "meta": { "page": 1, "limit": 20, "total": 42 }
}
```

## Catatan untuk AI Agent

- Frontend: jangan hardcode base URL, ambil dari `00_overview/STACK.md` atau env.
- Jika tambah endpoint baru, wajib ikut wrapper & pagination di atas, lalu update `API_REFERENCE.md`.
- Untuk Moodle backend, override bagian Wrapper & Auth dengan style `external_api` Moodle (lihat `STACK.md`).
