# API Reference

**Terakhir diupdate:** [YYYY-MM-DD]
**Base URL:** [https://api.example.com]

> Duplikat blok di bawah ini untuk tiap endpoint. Kelompokkan per resource (Users, Orders, dst) pakai heading `##`.

## Auth

[Jelaskan cara auth: Bearer token / API key / session cookie, dan cara mendapatkannya]

---

## Users

### `POST /users/register`
**Auth:** tidak perlu
**Deskripsi:** Registrasi user baru

**Request Body:**
```json
{
  "email": "string",
  "password": "string"
}
```

**Response 201:**
```json
{
  "id": "uuid",
  "email": "string"
}
```

**Error umum:**
| Status | Kondisi |
|---|---|
| 400 | Email sudah terdaftar |
| 422 | Validasi gagal |

---

### `[METHOD] /endpoint-berikutnya`
**Auth:**
**Deskripsi:**

**Request Body:**
```json
{}
```

**Response:**
```json
{}
```
