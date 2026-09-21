# Glosarium

> Daftar istilah domain project. AI wajib baca ini sebelum menulis kode agar tidak salah pakai istilah (misal: `order` vs `transaction`, `siswa` vs `peserta`).
> Bahasa: Indonesia. Tambah entry baru di bawah, urut abjad.

**Terakhir diupdate:** [YYYY-MM-DD]

| Istilah | Definisi | Sinonim / Jangan pakai | Catatan |
|---|---|---|---|
| User | Akun yang bisa login ke sistem | Jangan pakai `member` untuk ini | Bedakan dengan `Peserta` |
| Peserta | Orang yang ikut kelas/kursus, belum tentu punya akun User | | Relasi: `peserta.user_id → users.id` nullable |
| Kelas | Rombongan belajar, punya jadwal | Jangan pakai `class` di kode (reserved) → pakai `course_class` | |
| Transaksi | Pembayaran yang tercatat, status `pending/success/failed` | Jangan pakai `order` | |
| [Istilah kamu] | | | |

## Singkatan

| Singkatan | Kepanjangan | Konteks |
|---|---|---|
| LMS | Learning Management System | Moodle |
| VA | Virtual Account | Pembayaran |
| | | |

## Aturan untuk AI Agent

- Jika menemukan istilah baru di task/code yang belum ada di tabel, **tanya user** atau usulkan entry baru — jangan asumsi.
- Konsistensi: pakai istilah di kolom `Istilah` untuk nama variabel/tabel/kolom, bukan sinonim.
