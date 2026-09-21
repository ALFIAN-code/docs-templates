# Modul: Dashboard

**Terakhir diupdate:** [YYYY-MM-DD]
**Status:** Contoh — hapus file ini jika tidak pakai dashboard, atau ganti jadi modul kamu
**Lokasi kode:** `lib/features/dashboard/` (Flutter) / `src/modules/dashboard/` (web)
**Dependencies:** `auth`, `api`
**Dependents:** -

## Overview Modul

Dashboard adalah halaman utama setelah login. Menampilkan ringkasan data dan navigasi ke manajemen fitur lain. Modul ini contoh untuk pola **folder per modul kompleks** (lihat `AGENTS.md:9`).

> Jika modul kamu sederhana, cukup pakai 1 file `dashboard.md` dengan `### Fitur` di dalamnya. Contoh ini sengaja dipecah jadi folder karena punya >3 fitur.

## Daftar Fitur

| Fitur | Deskripsi | Dokumen |
|---|---|---|
| Analytics | Grafik, filter periode | [analytics.md](./analytics.md) |
| Manajemen User | List, tambah, edit user | [manajemen-user.md](./manajemen-user.md) |
| Ringkasan | Card statistik | (masih di file ini, belum dipecah) |

## Fitur: Ringkasan (contoh fitur yang masih di README)

- **Fungsi:** Menampilkan 4 card statistik (total user, transaksi hari ini, dll)
- **Lokasi:** `lib/features/dashboard/widgets/summary_cards.dart`
- **Flow:** `DashboardPage` → `SummaryProvider` → `GET /dashboard/summary` → render cards
- **Catatan:** Data di-cache 5 menit, lihat `CONVENTIONS.md` bagian cache.

## Catatan Penting untuk AI Agent

- Jangan ubah layout grid dashboard tanpa konfirmasi — dipakai di banyak role.
- Filter periode analytics pakai format `YYYY-MM-DD`, bukan timestamp.

## Checklist Saat Ubah Modul Ini

- [ ] Update file fitur terkait (`analytics.md` / `manajemen-user.md`) atau bagian di atas
- [ ] Update `ARCHITECTURE.md` jika tambah fitur besar
- [ ] Entry `PROGRESS_LOG.md`
