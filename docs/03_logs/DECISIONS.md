# Architecture Decision Records (ADR)

> Catat keputusan penting supaya tidak ditanyakan/diubah ulang tanpa sadar konsekuensinya.
> **Append entry baru di bawah, jangan hapus entry lama** — kalau sebuah keputusan berubah, buat entry baru dan tandai entry lama sebagai "Superseded by ADR-XXX".
>
> Ini file yang menangkap **hasil diskusi arsitektur**. Kalau ada keputusan yang diambil saat berdiskusi, tulis di sini **di turn yang sama** — jangan tunggu sesi selesai.

---

## Format Entry

```md
## ADR-NNN: [Judul keputusan, misal: "Pakai Riverpod, bukan Bloc"]

**Tanggal:** [YYYY-MM-DD] — dari `date "+%Y-%m-%d"`
**Status:** Proposed / Accepted / Deprecated / Superseded by ADR-XXX
**Dokumen terkait:** [ARCHITECTURE.md / STACK.md / UI_STYLE.md / modules/...]

**Konteks:**
[Masalah/kebutuhan apa yang mendorong keputusan ini diambil. Konteksnya sering lebih
penting daripada keputusannya — ini yang hilang duluan kalau cuma menyimpan "apa".]

**Keputusan:**
[Apa yang diputuskan, secara spesifik]

**Alternatif yang dipertimbangkan:**
- [Opsi A] — tidak dipilih karena [alasan]
- [Opsi B] — tidak dipilih karena [alasan]

**Konsekuensi:**
[Trade-off yang diterima, dampak ke development selanjutnya]

**Revisit jika:**
[Kapan keputusan ini perlu dibuka lagi — misal: "API berubah jadi cursor pagination"
atau "jumlah user > 10k". Kalau tidak ada kondisi ini, tulis "Tidak ada kondisi khusus".]
```

> **Status `Proposed`** dipakai saat keputusan masih dibahas di sesi yang sama. Ubah ke
> `Accepted` setelah user konfirmasi. Ini mencegah AI membangun implementasi di atas
> keputusan yang belum disepakati.

---

## ADR-001: [Judul keputusan, misal: "Pakai Riverpod, bukan Bloc"]

**Tanggal:** [YYYY-MM-DD]
**Status:** Proposed <!-- Proposed / Accepted / Deprecated / Superseded by ADR-XXX -->
**Dokumen terkait:** [STACK.md]

**Konteks:**
[Masalah/kebutuhan apa yang mendorong keputusan ini diambil]

**Keputusan:**
[Apa yang diputuskan, secara spesifik]

**Alternatif yang dipertimbangkan:**
- [Opsi A] — tidak dipilih karena [alasan]
- [Opsi B] — tidak dipilih karena [alasan]

**Konsekuensi:**
[Trade-off yang diterima, dampak ke development selanjutnya]

**Revisit jika:**
[Kapan keputusan ini perlu dibuka lagi. Kalau tidak ada kondisi khusus, tulis "Tidak ada kondisi khusus".]

---

## ADR-002: [Judul berikutnya]

**Tanggal:**
**Status:** Proposed / Accepted / Deprecated / Superseded by ADR-XXX
**Dokumen terkait:**

**Konteks:**

**Keputusan:**

**Alternatif yang dipertimbangkan:**

**Konsekuensi:**

**Revisit jika:**