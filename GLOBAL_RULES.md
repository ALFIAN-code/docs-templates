# Global Rules — Setup untuk Opencode & Antigravity (v3 Grouped + Modular Rules)

> Panduan setup global agar AI otomatis baca/tanya init `docs/` dengan aturan **anti copy-paste mentah** dan **style guide di 02_reference/**.

## Struktur Modular (WAJIB)

Rules dipisah dua lapis, supaya blok yang selalu aktif tetap **pendek** (lebih patuh) dan detail
hanya dimuat saat relevan (hemat context):

| Lapis | Isi | Kapan aktif |
|---|---|---|
| **Blok WAJIB** | `AGENTS.md` (~57 baris): mandatory blocker, konvensi status, default stack, aturan diskusi arsitektur | Selalu, semua project |
| **Rule guide** | `rules/*.md`: docs-workflow, flutter-stack, architecture-discussion | On-demand sesuai konteks |

## 1. Opencode

**Lokasi:** `~/.config/opencode/AGENTS.md` (blok wajib) + `~/.config/opencode/rules/` (3 guide)

`~/.config/opencode/opencode.json` mendaftarkan:

```json
"instructions": ["AGENTS.md"],
"references": {
  "my-rules":      { "path": "/Users/allvvnt/.config/opencode/rules", "description": "..." },
  "template-docs": { "path": "/Users/allvvnt/alfianSpace/files/agent-docs-template-v3", "description": "..." }
}
```

## 2. Antigravity

**Lokasi:** `~/.gemini/AGENTS.md` (blok wajib, mirror dari Opencode) + `~/.gemini/config/rules/` (3 guide)

Guide pakai YAML frontmatter dengan trigger berbeda — Antigravity cuma inline yang relevan:

| File | Trigger | Efek |
|---|---|---|
| `flutter-stack.md` | `glob: "*.dart, pubspec.yaml, analysis_options.yaml"` | Aktif **otomatis** saat menyentuh Dart, nol biaya kalau tidak |
| `architecture-discussion.md` | `model_decision` | Index + deskripsi saja; agent baca penuh saat task cocok |
| `docs-workflow.md` | `model_decision` | Idem, untuk init/migrasi docs |

> Frontmatter wajib. Tanpa `trigger` yang valid, file **diabaikan diam-diam**.
> Batas: 24 KB per file, 20.000 token agregat untuk `always_on` + `glob`.

> Jangan taruh rules bersama di `~/.gemini/GEMINI.md` — file itu dipakai bersama dengan
> Gemini CLI dan bisa konflik. Rules utama tetap di `AGENTS.md`.

## 3. Codex

**Lokasi:** `~/.codex/AGENTS.md` (terpasang, perlu update ke v3)

## Apa yang berubah di v3?

- `docs/` sekarang grouped: `00_overview/`, `01_guides/`, `02_reference/`, `03_logs/`, `modules/`
- `AGENTS.md` pindah ke **root project**, bukan `docs/`
- `STACK.md` sekarang di `00_overview/STACK.md` (merge 1 stack saja, folder `stacks/` tidak ke-copy)
- Style guide ada di `02_reference/API_STYLE.md` (wajib frontend) + `UI_STYLE.md` (wajib frontend — kontrak design system)
- **AI dilarang copy semua file mentah** — wajib cek manifest di `stacks/*.md` (Wajib/Opsional)

## Verifikasi setelah update

```bash
cat ~/.config/opencode/AGENTS.md | head -n 30
cat ~/.gemini/AGENTS.md | head -n 30
ls ~/.config/opencode/rules/ ~/.gemini/config/rules/
head -5 ~/.gemini/config/rules/flutter-stack.md   # cek frontmatter trigger
cat ~/.codex/AGENTS.md | head -n 30
ls -R /Users/allvvnt/alfianSpace/files/agent-docs-template-v3/docs
```

Setelah mengubah `opencode.json` atau file rules, **quit & restart opencode** — config
tidak hot-reload.

## Path Boilerplate v3

```
/Users/allvvnt/alfianSpace/files/agent-docs-template-v3
```

Jika `AGENTS.md:6` di project kosong, pakai fallback ini.
