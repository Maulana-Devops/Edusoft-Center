# LAPORAN PROGRESS PENGEMBANGAN

## Organizational Portfolio Platform

**Tanggal:** 1 Oktober 2026
**Project:** Organizational Portfolio Platform
**Pilot:** FAROIS Surakarta
**Status akhir:** M15 — Frontend & Public Experience Checkpoint

---

## 1. Ringkasan Kegiatan

Hari ini fokus pengembangan berada pada **penyelesaian Milestone 15 (M15) — Frontend & Public Experience Readiness**, khususnya penyelesaian audit accessibility dan pembuatan checkpoint Git untuk seluruh frontend redesign.

M15 sebelumnya telah diaudit dan ditemukan satu defect accessibility berupa **duplicate HTML `id` pada section halaman About**. Defect tersebut kemudian diperbaiki secara minimal tanpa mengubah arsitektur, API, backend, maupun desain yang sudah ada.

Setelah perbaikan divalidasi, seluruh perubahan frontend kemudian dibuat menjadi satu checkpoint Git terpisah.

---

# 2. Perbaikan Accessibility M15

### Masalah yang ditemukan

Pada halaman:

```text
web/src/pages/about.astro
```

tiga komponen `<Section>` sebelumnya tidak memberikan `id` eksplisit.

Akibatnya, `Section.astro` menggunakan fallback:

```text
section-title
```

sehingga beberapa section menggunakan `id` heading yang sama.

Hal tersebut menyebabkan:

* duplicate HTML IDs;
* beberapa `aria-labelledby` menunjuk ke heading yang sama;
* pembaca layar berpotensi mengumumkan judul section yang salah.

### Perbaikan

Ditambahkan tiga ID eksplisit:

| Section               | ID              |
| --------------------- | --------------- |
| Perjalanan organisasi | `perjalanan`    |
| Visi dan misi         | `visi-misi`     |
| Lokasi dan kontak     | `lokasi-kontak` |

Sehingga heading yang dihasilkan menjadi:

```text
perjalanan-title
visi-misi-title
lokasi-kontak-title
```

`Section.astro` **tidak diubah**. Perbaikan dilakukan sepenuhnya melalui API `id` yang memang sudah tersedia.

---

# 3. Validasi Accessibility

Setelah perbaikan dilakukan, halaman About dibangun ulang menggunakan data mock.

Hasil pemeriksaan:

```text
duplicate ids: NONE

aria-labelledby=perjalanan-title
→ Perjalanan organisasi

aria-labelledby=visi-misi-title
→ Visi dan misi

aria-labelledby=lokasi-kontak-title
→ Lokasi dan kontak
```

Selain itu dilakukan duplicate-ID sweep terhadap seluruh halaman hasil build dan tidak ditemukan duplicate ID.

Build tanpa data API juga berhasil dan tidak menghasilkan masalah accessibility baru.

---

# 4. Validasi Backend dan Regression

Walaupun perubahan hanya berada di frontend, regression test tetap dijalankan untuk memastikan perubahan tidak merusak platform secara keseluruhan.

### PostgreSQL

```text
551 passed
1 warning
```

Warning merupakan deprecation warning Starlette/AnyIO yang sudah ada sebelumnya.

### Tanpa database

```text
446 passed
105 skipped
1 warning
```

### Ruff

```text
All checks passed
```

### Build Astro

Dengan mock API:

```text
10 pages
0 warnings
0 errors
```

Tanpa API:

```text
10 pages
0 warnings
0 errors
```

---

# 5. Frontend Checkpoint

Setelah M15 dinyatakan siap, seluruh perubahan frontend yang sebelumnya masih berada di working tree dibuat menjadi satu checkpoint.

Commit:

```text
173ce93 feat: checkpoint M15 frontend redesign
```

Checkpoint tersebut mencakup:

* redesign seluruh public frontend;
* komponen UI baru;
* library frontend;
* layout dan navigasi;
* halaman public;
* styling dan design system;
* self-hosted font;
* accessibility fix M15.

### Statistik commit

```text
42 files changed
5977 insertions
1981 deletions
```

Seluruh file yang masuk commit berada di:

```text
web/
```

Tidak ada perubahan dari:

```text
core/
server/
infrastructure/
alembic/
tests/
docs/
```

yang ikut masuk checkpoint M15.

---

# 6. Verifikasi Git

Scope staging diverifikasi sebelum commit.

Hasil:

```text
Non-web staged files: NONE
Forbidden paths: NONE
```

Setelah commit:

```text
git status --short
```

menghasilkan working tree kosong.

Artinya:

**Working tree clean.**

Tidak dilakukan:

* push;
* amend;
* reset;
* stash;
* clean;
* revert.

Commit tetap berada secara lokal.

---

# 7. Catatan `git diff --check`

Terdapat satu laporan whitespace:

```text
web/public/fonts/OFL.txt:21
```

Baris tersebut merupakan bagian dari teks lisensi **SIL Open Font License 1.1** yang berasal dari distribusi font upstream.

File tidak diubah agar tetap mempertahankan teks lisensi sebagaimana didistribusikan.

Tidak terdapat whitespace issue lain pada perubahan aplikasi.

---

# 8. Kondisi Milestone Setelah Hari Ini

| Milestone   | Commit    | Status           |
| ----------- | --------- | ---------------- |
| M13.2–M13.5 | `a27b026` | Checkpointed     |
| M14         | `ff0f10b` | Checkpointed     |
| M15         | `173ce93` | **Checkpointed** |

HEAD saat ini:

```text
173ce93 feat: checkpoint M15 frontend redesign
```

Working tree:

```text
CLEAN
```

Remote:

```text
Belum di-push
```

---

# 9. Kesimpulan

Kegiatan hari ini berhasil menyelesaikan **M15 Frontend & Public Experience Readiness**.

Perbaikan utama adalah menyelesaikan defect accessibility pada halaman About dengan memberikan ID unik pada tiga section tanpa mengubah komponen `Section.astro` maupun arsitektur aplikasi.

Setelah itu seluruh frontend redesign berhasil divalidasi melalui build Astro, regression test PostgreSQL, Ruff, dan pemeriksaan Git.

Seluruh hasil frontend kemudian diamankan dalam checkpoint:

```text
173ce93 feat: checkpoint M15 frontend redesign
```

Dengan working tree yang sekarang bersih, project berada pada kondisi **stable checkpoint** dan siap memasuki milestone berikutnya.

**Status akhir hari ini: M15 CLOSED / CHECKPOINTED.**
