# AI Agent Rules — [Nama Project]

> File ini WAJIB di root project (bukan di dalam `docs/`). Dibaca AI agent (Opencode, Codex, dll) di **setiap awal sesi**, sebelum menulis kode apa pun.
> Alasan: AI tidak punya ingatan antar sesi. Folder `docs/` adalah pengganti ingatan tersebut — bukan opsional, tapi sumber kebenaran (source of truth).

**Cara pakai:**
- Simpan sebagai `AGENTS.md` di root project (Opencode & Codex baca otomatis).
- Jika pakai Claude Code juga → copy ke `CLAUDE.md` atau cukup `echo "@AGENTS.md" > CLAUDE.md`.

---

## 0. Prinsip Dasar

1. **Dokumentasi bukan hasil sampingan, tapi bagian dari definisi "selesai".** Task belum selesai kalau dokumentasi relevan belum diupdate.
2. **Jangan asumsi konteks dari chat sebelumnya.** Kalau tidak tertulis di `docs/`, anggap tidak pernah terjadi.
3. **Log itu append-only.** `03_logs/PROGRESS_LOG.md`, `03_logs/CHANGELOG.md`, `03_logs/DECISIONS.md` ditambah entry baru, bukan ditimpa/dihapus.
4. **Perubahan besar butuh persetujuan eksplisit**, bukan asumsi sepihak dari agent.
5. **Jangan copy-paste mentah.** Template punya banyak file, tapi tidak semua dibutuhkan. Ikuti `7. Mode Otonomi` dan `8. Stack Profile`.

---

## 1. SEBELUM Mulai Kerja (WAJIB, urutan baca)

Baca berurutan, jangan dilompat:

1. `docs/03_logs/PROGRESS_LOG.md` → baca 3-5 entry terakhir. "Ingatan jangka pendek": apa yang baru dikerjakan, status, next steps, blocker.
2. `docs/00_overview/STATE.md` → (jika ada) ringkasan 1 halaman status terkini untuk hemat context window. Jika tidak ada, baca `docs/00_overview/ARCHITECTURE.md` bagian Overview.
3. `docs/00_overview/ARCHITECTURE.md` → paham struktur sistem, tech stack, daftar modul. Ini **index**, detail tiap modul ada di `docs/modules/`.
4. `docs/00_overview/STACK.md` → cek stack aktif (misal: `flutter` atau `moodle`). File ini sudah berisi aturan stack yang terpilih (hasil merge dari `docs/stacks/*.md` di template). Lihat bagian 8.
5. `docs/02_reference/DATABASE_SCHEMA.md` → wajib kalau task menyentuh data/model/migration. Untuk frontend murni, file ini mungkin tidak ada (lihat manifest stack).
6. `docs/03_logs/DECISIONS.md` → cek keputusan teknis yang membatasi pendekatan.
7. `docs/01_guides/GLOSSARY.md` + `docs/01_guides/CONVENTIONS.md` → cek istilah domain dan aturan penamaan.
8. `docs/02_reference/API_STYLE.md` → jika ada (khusus frontend), cek style wrapper API sebelum call endpoint.

**Jika salah satu file di atas belum ada / masih kosong:**
- Jangan langsung menebak atau membuat file baru diam-diam.
- Tanya user dulu, atau scan codebase dan **konfirmasi ke user** sebelum lanjut. Lihat bagian 7 (L1).

**Jika instruksi user di chat bertentangan dengan `DECISIONS.md`:** Konfirmasi eksplisit sebelum override.

## 2. SELAMA Development

- Kerjakan dalam unit kecil yang mudah direview, bukan satu perubahan raksasa.
- Jangan ubah schema database, arsitektur inti, konvensi penamaan, atau pattern di `docs/` tanpa persetujuan eksplisit.
- Untuk hal berdampak besar (auth, payment, migrasi data, breaking change) → tanya dulu.
- Beri comment pada logic yang tidak obvious, terutama workaround atau edge case.
- Jangan tambah dependency baru tanpa menyebutkannya ke user (dan catat alasannya di `DECISIONS.md` jika signifikan).
- Jika mengerjakan fitur dalam 1 modul di `docs/modules/`, baca file modul tersebut dulu. Jika modul belum ada dokumentasinya, tawarkan untuk membuatkannya (jangan langsung create di L1).

## 3. SETELAH Selesai Task (WAJIB sebelum bilang "selesai" ke user)

Update dokumen sesuai jenis perubahan:

| Jenis perubahan | Dokumen yang diupdate |
|---|---|
| Struktur sistem, folder baru, module/service baru | `docs/00_overview/ARCHITECTURE.md` (index) + `docs/modules/[nama].md` atau `docs/modules/[nama]/README.md` |
| Fitur baru / perubahan logic dalam 1 modul | `docs/modules/[nama].md` atau `docs/modules/[nama]/[fitur].md` |
| Tabel baru, kolom baru, relasi, migration | `docs/02_reference/DATABASE_SCHEMA.md` |
| Endpoint API baru / berubah | `docs/02_reference/API_REFERENCE.md` |
| Style API / kontrak response berubah | `docs/02_reference/API_STYLE.md` |
| Style UI / design token berubah | `docs/02_reference/UI_STYLE.md` |
| Istilah baru / definisi domain | `docs/01_guides/GLOSSARY.md` |
| Aturan coding baru | `docs/01_guides/CONVENTIONS.md` |
| **Setiap sesi kerja (selalu)** | `docs/03_logs/PROGRESS_LOG.md` + update `docs/00_overview/STATE.md` jika ada |
| Keputusan teknis penting | `docs/03_logs/DECISIONS.md` |
| Perubahan user-facing | `docs/03_logs/CHANGELOG.md` |

Agent **tidak boleh** klaim selesai tanpa update di atas.

**Checklist sebelum close sesi:**
- [ ] `03_logs/PROGRESS_LOG.md` entry baru di paling atas?
- [ ] `00_overview/ARCHITECTURE.md` atau `docs/modules/*` sinkron?
- [ ] `00_overview/STATE.md` diupdate?
- [ ] Tidak ada file `docs/` yang basi?

## 4. Format Entry `PROGRESS_LOG.md`

Tambahkan entry baru di **paling atas** (setelah heading), format:

```
## [YYYY-MM-DD HH:mm] Judul singkat task
**Status:** Selesai / Sebagian / Blocked
**Dikerjakan:**
- poin 1
**File yang diubah:**
- path/to/file.ts
**Dokumen yang diupdate:**
- docs/... 
**Belum selesai / next steps:**
- poin
**Catatan/masalah:**
- poin
```

## 5. Larangan

- Jangan hapus/timpa history di `03_logs/` (append-only).
- Jangan buat dokumentasi duplikat di luar `docs/` (misal README kedua yang beda dari `ARCHITECTURE.md`).
- Jangan bilang "sudah saya jelaskan sebelumnya" — kalau penting, harusnya ada di `docs/`.
- Jangan generate dokumentasi asal panjang. Singkat, akurat, berguna untuk sesi berikutnya.
- Jangan membuat file/folder baru di `docs/` tanpa konfirmasi di L1 (lihat bagian 7).

---

## 6. Info Project (isi manual oleh developer)

- **Nama project:**
- **Deskripsi singkat:**
- **Tech stack:**
- **Tipe stack:** `frontend` / `backend` / `fullstack` (untuk tentukan kebutuhan dokumen, lihat bagian 8)
- **Stack profile aktif:** `flutter` / `moodle` / `nextjs` / `custom` (isinya sudah di-merge ke `docs/00_overview/STACK.md`)
- **Command penting:**
  - `install:`
  - `dev:`
  - `test:`
  - `build:`
  - `migrate:`
- **Area yang tidak boleh diubah tanpa izin:**
- **Path boilerplate template:** `/Users/allvvnt/alfianSpace/files/agent-docs-template-v3` (dipakai AI saat init - lihat bagian 7)

---

## 7. Mode Otonomi (Default: L1 Supervised)

| Level | Nama | Perilaku AI |
|---|---|---|
| **L0** | Human-led | Selalu tanya sebelum ubah kode/docs apa pun. |
| **L1** | **Supervised (Default)** | Boleh ubah kode sesuai task, tapi **wajib tanya dulu** sebelum: (a) init `docs/` dari boilerplate, (b) buat file baru di `docs/`, (c) tambah stack baru, (d) ubah `DECISIONS.md`. |
| **L2** | Full-auto | Boleh langsung init & update tanpa tanya. Hanya pakai jika full supervised via review. |

### Aturan Anti Copy-Paste Mentah (WAJIB untuk v3)

Template `agent-docs-template-v3` punya banyak file, tapi **JANGAN copy semua mentah ke project**.

Saat init `docs/`:

1. **Baca dulu** `docs/stacks/[terpilih].md` di template bagian **“Kebutuhan Dokumen”** (tabel Wajib/Opsional).
2. **Hanya copy file yang `Wajib = Ya`** untuk tipe stack tersebut.
   - Contoh Flutter (`frontend`): `00_overview/*`, `01_guides/*`, `03_logs/*`, `02_reference/API_REFERENCE.md`, `02_reference/API_STYLE.md`, `modules/_template.md` → **jangan copy** `02_reference/DATABASE_SCHEMA.md` dan `02_reference/SECURITY_AND_DATA.md` kecuali user minta.
   - Contoh Moodle (`backend`): semua `02_reference/*` wajib termasuk `DATABASE_SCHEMA.md`.
3. **File `Opsional`** → tanya user: “`UI_STYLE.md` belum ada, mau saya buatkan? Ini untuk design system.” Jangan langsung buat.
4. **Jika stack baru** (tidak ada di template) → tentukan `tipe: frontend/backend/fullstack` dari codebase, lalu pakai rule fallback di `docs/stacks/_template.md`. Tetap konfirmasi ke user.
5. **Folder `stacks/` tidak di-copy ke project.** Hanya 1 file stack yang terpilih di-merge jadi `docs/00_overview/STACK.md`. Jadi project Flutter tidak akan punya `moodle.md` di dalamnya.

**Jika `docs/` belum ada saat sesi dimulai (L1):**
1. Jangan `mkdir docs/`.
2. Tanya: "`docs/` belum ditemukan. Mau saya init dari boilerplate di `[path AGENTS.md:6]`? Default: `/Users/allvvnt/alfianSpace/files/agent-docs-template-v3`. Saya akan hanya copy file yang dibutuhkan untuk stack `[terdeteksi/manual]` — tidak semua."
3. Tunggu konfirmasi. Jika YA, tawarkan stack mana (deteksi `pubspec.yaml` → flutter, `version.php` → moodle).

## 8. Stack Profile (Hybrid + Manifest)

Setiap project hasil init punya 1 file: `docs/00_overview/STACK.md` (bukan `docs/STACK.md` lagi).

**Cara kerja:**

1. Saat init, AI deteksi stack atau tanya user. Jika deteksi `pubspec.yaml` → tawarkan `flutter.md`, `version.php` → `moodle.md`.
2. AI baca `agent-docs-template-v3/docs/stacks/[nama].md` → lihat tabel Kebutuhan Dokumen → copy selective.
3. Isi `stacks/[nama].md` di-template di-merge jadi `docs/00_overview/STACK.md` di project (jadi project tidak bawa folder `stacks/`).
4. Jika project butuh ganti stack / tambah stack kedua, edit `docs/00_overview/STACK.md` dan tanya user.

**Isi tiap `docs/stacks/*.md`:** aturan spesifik stack (struktur folder, command, library, plus tabel Kebutuhan Dokumen). Lihat `flutter.md` dan `moodle.md`.

## 9. Aturan Modular (ARCHITECTURE + modules/)

`docs/00_overview/ARCHITECTURE.md` adalah **index**, detail ada di `docs/modules/`.

| Kondisi | Struktur |
|---|---|
| Modul sederhana (1-3 fitur, <200 baris) | `docs/modules/[nama].md` — grouping `### Fitur` di dalamnya |
| Modul kompleks (>3 fitur) | `docs/modules/[nama]/README.md` + `docs/modules/[nama]/[fitur].md` per fitur |

Jika 1 fitur punya sub-grouping lagi (misal `dashboard > analytics > filter-periode`), pakai `#### Sub-fitur` di dalam file fitur — jangan nesting folder >2 level.

**Alur AI:** Dapat task “buat fitur X di dashboard” → baca `docs/modules/dashboard/README.md` dulu. Jika belum ada → tanya mau dibikinkan dari `modules/_template.md`?
