# Global Rules — Setup untuk Opencode & Codex (v3 Grouped + Selective Copy)

> Panduan setup global agar AI otomatis baca/tanya init `docs/` dengan aturan **anti copy-paste mentah** dan **style guide di 02_reference/**.
> Kamu pakai Opencode + Codex (bukan Claude Code).

## 1. Opencode

**Lokasi:** `~/.config/opencode/AGENTS.md` (sudah terpasang, perlu update ke v3)

File global opencode akan saya update otomatis ke versi v3 di bawah.

## 2. Codex

**Lokasi:** `~/.codex/AGENTS.md` (sudah terpasang, perlu update ke v3)

## Apa yang berubah di v3?

- `docs/` sekarang grouped: `00_overview/`, `01_guides/`, `02_reference/`, `03_logs/`, `modules/`
- `AGENTS.md` pindah ke **root project**, bukan `docs/`
- `STACK.md` sekarang di `00_overview/STACK.md` (merge 1 stack saja, folder `stacks/` tidak ke-copy)
- Style guide ada di `02_reference/API_STYLE.md` (wajib frontend) + `UI_STYLE.md` (opsional)
- **AI dilarang copy semua file mentah** — wajib cek manifest di `stacks/*.md` (Wajib/Opsional)

## Verifikasi setelah update

```bash
cat ~/.config/opencode/AGENTS.md | head -n 30
cat ~/.codex/AGENTS.md | head -n 30
ls -R /Users/allvvnt/alfianSpace/files/agent-docs-template-v3/docs
```

## Path Boilerplate v3

```
/Users/allvvnt/alfianSpace/files/agent-docs-template-v3
```

Jika `AGENTS.md:6` di project kosong, pakai fallback ini.
