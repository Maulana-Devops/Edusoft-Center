# LAPORAN AKTIVITAS PKL

**Nama:** Maulana Aldi Pradana
**Tanggal:** Selasa, 29 September 2026
**Program:** Simulasi Industri Junior Data Analyst
**Fokus:** Dokumentasi Proyek, Quality Control Repository, dan Portfolio

---

## 1. Sinkronisasi Learning Journal

Melakukan pembaruan terhadap dokumentasi:

`docs/learning-journal.md`

Pembaruan dilakukan untuk menyelaraskan catatan progress pembelajaran dengan kondisi repository yang sebenarnya.

Progress Tracker diperbarui untuk mencakup:

* Week 1 — Not in repo
* Week 2 — Completed
* Week 3 — Not in repo
* Week 4 — Completed
* Week 5 — Completed
* Week 6 — Completed
* Week 7 — Completed
* Week 8 — Completed
* Week 9 — Completed
* Week 10 — Completed
* Week 11 — Completed
* Week 12 — Completed
* Final Project — Completed

Dalam proses ini, tidak menambahkan aktivitas atau refleksi yang tidak memiliki evidence di repository.

---

## 2. Pembaruan Weekly Summary

Bagian Weekly Summary pada Learning Journal disesuaikan dengan Progress Tracker.

Tujuannya agar dokumentasi:

* konsisten antarbagian;
* mencerminkan folder dan deliverable yang benar-benar tersedia;
* tidak memberikan klaim terhadap Week 1 dan Week 3 yang tidak terdapat di repository.

---

## 3. Perbaikan Final Reflection

Bagian Final Reflection diperbarui agar sesuai dengan status terbaru program.

Learning Journal sekarang merepresentasikan repository sebagai dokumentasi perjalanan pembelajaran yang telah mencapai:

**Week 12 + Final Project.**

Refleksi juga tetap dibuat terbuka untuk diperbarui apabila terdapat pembelajaran atau perkembangan baru.

---

## 4. Audit README

Melakukan pengecekan terhadap `README.md` dan membandingkannya dengan:

`docs/Project Structure.md`

Ditemukan deskripsi lama yang sudah tidak sesuai dengan kondisi dokumentasi terbaru.

Deskripsi tersebut diperbaiki sehingga menjelaskan bahwa `Project Structure.md` mencakup:

1. Actual Repository Structure
2. Canonical Final Project Structure
3. Historical Weekly Structure
4. Planned Repository Structure

Dengan demikian README dan Project Structure kembali konsisten.

---

## 5. Quality Control Repository

Sebelum melakukan commit, dilakukan pemeriksaan perubahan menggunakan:

```bash
git diff --check
git diff --stat
git diff --name-status
git status --short
```

Hasil pemeriksaan menunjukkan hanya dua file yang berubah:

```text
README.md
docs/learning-journal.md
```

Tidak terdapat perubahan terhadap source code, dataset, notebook, maupun deliverable Final Project.

---

## 6. Commit Dokumentasi

Setelah perubahan dinyatakan sesuai scope, dilakukan commit:

```text
b15cfee docs: synchronize project progress documentation
```

Isi commit:

```text
2 files changed
68 insertions(+)
24 deletions(-)
```

Commit hanya mencakup pembaruan dokumentasi proyek PKL.

---

## 7. Push dan Sinkronisasi GitHub

Commit kemudian dikirim ke repository GitHub menggunakan:

```bash
git push origin main
```

Push berhasil.

Setelah itu dilakukan verifikasi:

```bash
git fetch origin
git status --short
git rev-parse HEAD
git rev-parse origin/main
```

Hasil:

```text
HEAD        = b15cfee
origin/main = b15cfee
```

Working tree dalam kondisi bersih.

Dengan demikian repository lokal dan repository GitHub telah kembali sinkron.

---

## 8. Pengembangan Portfolio Pendukung PKL

Selain repository Data Analyst, pekerjaan PKL juga mencakup kelanjutan pengembangan **Organizational Portfolio Platform** sebagai proyek portfolio teknologi.

Proyek tersebut dikembangkan sebagai platform reusable untuk organisasi dan telah memasuki tahap validasi deployment.

Production smoke test dilakukan terhadap deployment:

`portofolio-organisasi.vercel.app`

Salah satu hasil validasi:

```text
--- API ---
PASS API health
```

Validasi ini digunakan untuk memastikan komponen utama aplikasi dapat berjalan pada environment production.

---

## 9. Pembelajaran Hari Selasa

Beberapa pembelajaran yang diperoleh:

### Dokumentasi Proyek

* Dokumentasi harus mengikuti kondisi repository aktual.
* Planned structure dan actual structure harus dibedakan.
* Progress harus didasarkan pada evidence.
* Informasi yang tidak tersedia tidak boleh dibuat berdasarkan asumsi.

### Git/GitHub

* Melakukan audit diff sebelum commit.
* Membatasi scope commit sesuai pekerjaan.
* Memastikan working tree bersih.
* Memverifikasi kesamaan `HEAD` dan `origin/main` setelah push.

### Portfolio Engineering

* Dokumentasi merupakan bagian dari kualitas portfolio.
* Deployment perlu diuji menggunakan smoke test.
* Status aplikasi production perlu diverifikasi berdasarkan hasil pengujian, bukan asumsi.

---

## 10. Hasil Akhir Hari Selasa

Pada akhir aktivitas PKL, diperoleh hasil:

* ✅ Learning Journal diperbarui.
* ✅ Progress Week 1–12 dan Final Project diselaraskan.
* ✅ README diperbaiki.
* ✅ Dokumentasi Project Structure kembali konsisten.
* ✅ Perubahan diaudit sebelum commit.
* ✅ Commit `b15cfee` berhasil dibuat.
* ✅ Perubahan berhasil dipush ke GitHub.
* ✅ Local repository dan GitHub repository sinkron.
* ✅ Working tree bersih.
* ✅ Production smoke test Organizational Portfolio Platform menunjukkan API health **PASS**.

**Kesimpulan:**
Aktivitas PKL hari Selasa berfokus pada **quality control, dokumentasi, version control, dan penguatan portfolio proyek**. Pekerjaan tidak hanya memastikan hasil analisis terdokumentasi, tetapi juga memastikan repository dapat dipertanggungjawabkan secara teknis dan siap menjadi bagian dari portfolio profesional.
