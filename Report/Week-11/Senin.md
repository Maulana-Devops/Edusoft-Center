# LAPORAN AKTIVITAS HARIAN

**Nama:** Maulana Aldi Pradana
**Tanggal:** Senin, 28 September 2026
**Fokus:** Data Analyst, Dokumentasi Proyek, Git/GitHub, dan Pengembangan Proyek Lain

---

## 1. Kegiatan Utama — Proyek Data Analyst

Pada hari Senin, kegiatan utama difokuskan pada melanjutkan **Final Project Data Analyst**, khususnya tahap pengolahan dan persiapan data untuk analisis.

### A. Data Cleaning

Melakukan pemeriksaan dan pengolahan dataset Indonesia E-Commerce Sales yang digunakan dalam Final Project.

Hasil utama:

* Dataset raw berjumlah **18.868 baris dan 19 kolom**.
* Dataset hasil cleaning berjumlah **18.868 baris dan 30 kolom**.
* Melakukan pemeriksaan struktur dan tipe data.
* Melakukan validasi data tanggal.
* Memeriksa kemungkinan data duplikat.
* Menangani format data pembayaran.
* Menangani missing value pada data pembayaran dengan kategori **"Tidak Diketahui"**.
* Mempertahankan missing value pada `total_qty` ketika tidak terdapat dasar yang cukup untuk melakukan imputasi.
* Mendokumentasikan proses cleaning melalui **Data Cleaning Log**.

### B. Menentukan Batasan Data

Dilakukan pengecekan agar analisis tidak menghasilkan informasi yang tidak tersedia dalam dataset.

Beberapa data yang tidak tersedia secara valid tidak dibuat secara artifisial, seperti:

* Customer ID
* Profit
* Cost
* informasi customer tambahan

Keterbatasan tersebut diperlakukan sebagai bagian dari **data limitation**, bukan diisi dengan data buatan.

### C. Persiapan Exploratory Data Analysis

Setelah data cleaning, dataset mulai dipersiapkan untuk tahap **Exploratory Data Analysis (EDA)**.

Beberapa KPI awal yang dihitung:

| KPI               |         Hasil |
| ----------------- | ------------: |
| Revenue           | Rp962.091.801 |
| Orders            |        18.868 |
| Quantity          |        47.688 |
| AOV               |    ± Rp50.991 |
| Cancellation Rate |        13,64% |
| Return Rate       |         0,76% |

Analisis awal mencakup:

* Revenue
* Orders
* Quantity
* Average Order Value
* Cancellation
* Return
* Discount
* tren penjualan
* performa kategori produk
* performa wilayah
* metode pembayaran

---

## 2. Dokumentasi Final Project

Selain analisis, dilakukan pemeriksaan terhadap struktur dokumentasi Final Project agar hasil pekerjaan dapat ditelusuri dengan jelas.

Struktur canonical Final Project yang digunakan:

```text
docs/Final Project/
├── 01_Project_Charter/
├── 02_Data/
│   ├── Raw_Dataset/
│   └── Clean_Dataset/
├── 03_Data_Cleaning/
├── 04_Analysis/
├── 05_Business_Analysis/
├── 06_Dashboard/
├── 07_Report/
├── 08_Presentation/
└── 09_Portfolio/
```

Struktur tersebut digunakan sebagai acuan dokumentasi hasil akhir proyek.

---

## 3. Dokumentasi Repository

Dilakukan pemeriksaan dan sinkronisasi beberapa dokumen repository.

### `docs/Project Structure.md`

Dokumen diperjelas untuk membedakan:

1. Struktur repository aktual.
2. Struktur canonical Final Project.
3. Folder historical weekly project.
4. Struktur repository yang sebelumnya direncanakan.

### `docs/Roadmap.md`

Progress program diperiksa agar sesuai dengan implementasi repository sampai Week 12 dan Final Project.

### `docs/References.md`

Referensi proyek diperbaiki dengan membedakan:

* teknologi/library yang benar-benar memiliki evidence penggunaan;
* dependency yang tercantum tetapi belum memiliki evidence penggunaan langsung.

Tujuannya agar dokumentasi portfolio tidak membuat klaim penggunaan teknologi yang tidak dapat dibuktikan dari repository.

---

## 4. Audit Repository Git

Dilakukan pemeriksaan kondisi repository sebelum perubahan dokumentasi.

Beberapa pemeriksaan yang digunakan:

```bash
git diff --check
git diff --stat
git diff --name-status
git status --short
```

Tujuannya memastikan perubahan yang dilakukan hanya berada pada scope pekerjaan yang direncanakan dan tidak terdapat perubahan tidak disengaja.

---

## 5. Pekerjaan Proyek Lain

Selain Data Analyst, hari Senin juga digunakan untuk melanjutkan pekerjaan pada **Organizational Portfolio Platform**.

Proyek tersebut tetap dikembangkan sebagai platform portfolio organisasi yang reusable dan tidak dibuat khusus hanya untuk satu organisasi.

Pekerjaan berfokus pada melanjutkan pengembangan dan validasi proyek yang sebelumnya sudah mencapai tahap production testing.

---

## 6. Hasil Pembelajaran Hari Senin

Beberapa hal yang dipelajari dan diperkuat:

### Data Analyst

* Pentingnya melakukan data validation sebelum EDA.
* Tidak semua missing value harus diisi.
* Analisis harus mengikuti informasi yang benar-benar tersedia dalam dataset.
* Data limitation perlu didokumentasikan.
* KPI harus memiliki dasar perhitungan yang jelas.

### Git/GitHub

* Setiap perubahan repository perlu diaudit sebelum commit.
* `git diff --check` digunakan untuk memeriksa masalah whitespace.
* `git diff --name-status` membantu memastikan file yang berubah sesuai scope.
* Dokumentasi project juga perlu diperlakukan sebagai bagian dari quality control.

### Dokumentasi

* README harus selalu konsisten dengan kondisi repository sebenarnya.
* Planned structure dan actual structure perlu dibedakan.
* Evidence repository lebih penting daripada asumsi ketika mendokumentasikan progress.

---

## 7. Ringkasan Hasil Hari Senin

Pada akhir hari Senin, pekerjaan utama yang telah dilakukan adalah:

* ✅ Melanjutkan data cleaning Final Project.
* ✅ Menghasilkan clean dataset.
* ✅ Melakukan validasi data.
* ✅ Menghitung KPI awal.
* ✅ Mempersiapkan tahap EDA.
* ✅ Memeriksa batasan dataset.
* ✅ Memeriksa struktur Final Project.
* ✅ Mengaudit dokumentasi repository.
* ✅ Melanjutkan pekerjaan Organizational Portfolio Platform.
* ✅ Melakukan quality control terhadap perubahan repository.

**Kesimpulan:**
Hari Senin difokuskan pada penguatan fondasi Final Project Data Analyst melalui data cleaning, validasi, dan persiapan EDA, sekaligus memperbaiki kualitas dokumentasi dan struktur repository agar proyek lebih siap digunakan sebagai portfolio. Pekerjaan teknis lain pada Organizational Portfolio Platform juga tetap dilanjutkan secara paralel.
