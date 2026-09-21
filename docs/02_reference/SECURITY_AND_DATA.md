# Keamanan & Data

> Kebijakan keamanan, privacy, dan pengelolaan data. Opsional untuk frontend murni, wajib untuk backend yang simpan data sensitif.
> Bahasa: Indonesia.

**Terakhir diupdate:** [YYYY-MM-DD]

## Data Sensitif

| Data | Lokasi | Enkripsi | Retensi |
|---|---|---|---|
| Password | `users.password` | hash bcrypt | permanen sampai user hapus |
| Token | `device_tokens` | at rest | 30 hari |
| [isi] | | | |

## Auth & Session

- Metode: [JWT / Session / Moodle token]
- Expiry: [misal: access 15m, refresh 7d]
- Storage frontend: [SecureStorage / localStorage — jangan plain]

## Validasi & Sanitasi

- Validasi di layer: [service, bukan controller]
- Sanitasi input: [htmlspecialchars / DOMPurify, dll]

## Capability / Role (khusus Moodle/backend)

| Role | Capability | Catatan |
|---|---|---|
| admin | `local/plugin:manage` | |
| | | |

## Logging & Audit

- Apa yang di-log: [login, ubah data sensitif]
- Dimana: [table `audit_logs` atau file]

## Catatan untuk AI Agent

- Jangan log data sensitif (password, token) ke console/file.
- Jika tambah field sensitif, update tabel di atas + `DATABASE_SCHEMA.md`.
