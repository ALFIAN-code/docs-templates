# Stack Profile: Moodle — Backend/LMS Plugin

> Template stack untuk Moodle LMS / plugin Moodle. Saat init project Moodle, AI akan merge isi ini ke `docs/00_overview/STACK.md` dan hanya copy file yang Wajib sesuai tabel (AGENTS.md:7).
> Bahasa: Indonesia.

**Tipe:** `backend` (LMS)
**Moodle version:** [4.3.x]
**PHP version:** [8.1]
**DB:** [PostgreSQL / MySQL]

## Kebutuhan Dokumen (Manifest — Dipakai AI untuk Selective Copy)

| Kategori | File | Wajib? | Alasan |
|---|---|---|---|
| 00_overview | `ARCHITECTURE.md`, `STATE.md`, `STACK.md` | Ya | inti |
| 03_logs | `PROGRESS_LOG.md`, `DECISIONS.md`, `CHANGELOG.md` | Ya | history |
| 01_guides | `GETTING_STARTED.md`, `CONVENTIONS.md`, `GLOSSARY.md` | Ya | onboarding |
| 01_guides | `WORKFLOW.md` | Opsional | tanya |
| 02_reference | `API_REFERENCE.md` | Ya | web service `external_api` / REST Moodle |
| 02_reference | `API_STYLE.md` | Ya | **wajib backend Moodle**: `wstoken`, `wsfunction`, `required_param()` |
| 02_reference | `UI_STYLE.md` | Tidak | backend tidak butuh design system. Jika plugin ada UI (Behat), tanya dulu |
| 02_reference | `DATABASE_SCHEMA.md` | Ya | **wajib**: `install.xml`, `upgrade.php`, ERD |
| 02_reference | `SECURITY_AND_DATA.md` | Ya | `access.php`, capability, privacy API |
| modules | `modules/_template.md` | Ya | template per plugin/fitur |

**Ringkasan untuk AI:** Moodle = backend → `02_reference` lengkap termasuk DB & Security. `UI_STYLE` tidak perlu.

---

## Struktur Plugin Wajib

```
local/nama_plugin/ atau mod/nama_plugin/
├── version.php         # WAJIB — bump version YYYYMMDDXX jika ubah DB/capability
├── db/
│   ├── install.xml
│   ├── upgrade.php     # append only, jangan edit step lama
│   └── access.php
├── classes/
│   ├── external/       # API
│   └── ...
├── lang/en/
└── ...
```

**Larangan:** Jangan ubah core `lib/`, `admin/` — hanya via plugin.

## Command

| Perlu | Command |
|---|---|
| Install fresh | `php admin/cli/install_database.php --agree-license` |
| Upgrade | `php admin/cli/upgrade.php --non-interactive` |
| Purge cache | `php admin/cli/purge_caches.php` |
| Cron | `php admin/cli/cron.php` |

## Version & Upgrade (Sering Error)

- Ubah schema/capability → naikkan `$plugin->version` di `version.php`.
- Tambah step di `db/upgrade.php` dengan `if ($oldversion < YYYYMMDDXX)` — **jangan edit lama**.
- Wajib sebut version bump di `03_logs/PROGRESS_LOG.md` dan `02_reference/DATABASE_SCHEMA.md`.

## Library / API Moodle

- Pakai `$DB` (`moodle_database`), jangan raw `mysqli`.
- Pakai `external_api` untuk web service, cek capability.
- String via `get_string()`, jangan hardcode.

## Konvensi Khusus Moodle

- File PHP: `snake_case.php`, class `PascalCase` di `classes/`
- Namespace: `local_nama_plugin\`
- Capability: `local/nama:capname` di `db/access.php`
- Jangan `$_GET`/`$_POST` langsung → pakai `required_param()`.

## Checklist Sebelum Selesai

- [ ] `version.php` bump jika ubah DB/capability?
- [ ] `db/upgrade.php` step baru append?
- [ ] `02_reference/DATABASE_SCHEMA.md` update?
