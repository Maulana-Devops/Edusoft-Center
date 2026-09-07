# LAPORAN WEEK 8

## GroupBy dan Aggregation dengan Pandas untuk Analisis Data

**Nama:** Maulana Aldi Pradana
**Program:** Data Analyst
**Minggu:** Week 8
**Tanggal:** 8 September 2026
**Topik:** GroupBy dan Aggregation dengan Pandas

---

## 1. Tujuan Kegiatan

Pada Week 8, kegiatan difokuskan pada penggunaan **GroupBy dan Aggregation pada Pandas** untuk mengolah data menjadi informasi yang lebih mudah dianalisis.

Tujuan kegiatan ini adalah:

* Memahami konsep pengelompokan data menggunakan `groupby()`.
* Mengelompokkan data berdasarkan kategori tertentu.
* Menghitung nilai agregasi seperti jumlah, rata-rata, minimum, maksimum, dan jumlah data.
* Menggunakan beberapa fungsi agregasi secara bersamaan.
* Mengurutkan hasil analisis untuk menemukan kelompok dengan performa tertinggi maupun terendah.
* Mengubah hasil pengolahan data menjadi informasi yang dapat digunakan untuk analisis bisnis.

---

## 2. Materi yang Dipelajari

Materi utama yang dipelajari pada Week 8 adalah:

### A. GroupBy

`groupby()` digunakan untuk mengelompokkan data berdasarkan satu atau beberapa kolom.

Contoh:

```python
df.groupby("kategori")
```

Pengelompokan ini memungkinkan analisis dilakukan pada masing-masing kelompok data.

### B. Aggregation

Setelah data dikelompokkan, digunakan fungsi agregasi seperti:

```python
sum()
mean()
count()
min()
max()
```

Contohnya:

```python
df.groupby("kategori")["penjualan"].sum()
```

Kode tersebut digunakan untuk menghitung total penjualan berdasarkan setiap kategori.

### C. Multiple Aggregation

Beberapa fungsi agregasi dapat digunakan secara bersamaan menggunakan `.agg()`.

Contoh:

```python
df.groupby("kategori")["penjualan"].agg(
    ["sum", "mean", "min", "max", "count"]
)
```

Hasilnya dapat digunakan untuk membandingkan karakteristik setiap kelompok data.

### D. Sorting

Hasil agregasi dapat diurutkan menggunakan `sort_values()`.

Contoh:

```python
hasil = df.groupby("kategori")["penjualan"].sum()

hasil.sort_values(ascending=False)
```

Dengan pengurutan tersebut, kategori dengan total penjualan terbesar dapat ditemukan dengan lebih mudah.

---

## 3. Tahapan Praktik

### Langkah 1 — Menyiapkan Dataset

Dataset penjualan digunakan sebagai bahan praktik analisis.

Dataset diperiksa terlebih dahulu untuk memastikan kolom yang akan digunakan tersedia dan memiliki tipe data yang sesuai.

Contoh:

```python
import pandas as pd

df = pd.read_csv("sales_data.csv")

df.head()
```

---

### Langkah 2 — Melihat Struktur Dataset

Struktur dataset diperiksa menggunakan:

```python
df.info()
```

Selain itu, beberapa baris awal dataset ditampilkan menggunakan:

```python
df.head()
```

Tahap ini dilakukan untuk memahami nama kolom dan struktur data sebelum melakukan pengelompokan.

---

### Langkah 3 — Melakukan GroupBy

Data dikelompokkan berdasarkan kolom kategori.

```python
df.groupby("kategori")
```

Untuk memperoleh jumlah data pada setiap kategori:

```python
df.groupby("kategori").size()
```

Hasil tersebut menunjukkan jumlah record yang terdapat pada masing-masing kelompok.

---

### Langkah 4 — Menghitung Total dengan Sum

Untuk mengetahui total nilai penjualan berdasarkan kategori:

```python
df.groupby("kategori")["penjualan"].sum()
```

Hasilnya dapat digunakan untuk mengetahui kategori yang memberikan kontribusi penjualan terbesar.

---

### Langkah 5 — Menghitung Rata-Rata dengan Mean

Selain total, rata-rata penjualan juga dapat dihitung:

```python
df.groupby("kategori")["penjualan"].mean()
```

Analisis ini membantu mengetahui nilai rata-rata penjualan pada setiap kategori.

---

### Langkah 6 — Menggunakan Multiple Aggregation

Beberapa statistik dapat dihitung sekaligus:

```python
hasil = df.groupby("kategori")["penjualan"].agg(
    ["sum", "mean", "min", "max", "count"]
)

hasil
```

Dengan cara ini, analisis setiap kategori dapat dilakukan secara lebih lengkap dalam satu tabel.

---

### Langkah 7 — Mengurutkan Hasil

Untuk menemukan kategori dengan total penjualan tertinggi:

```python
hasil_penjualan = (
    df.groupby("kategori")["penjualan"]
    .sum()
    .sort_values(ascending=False)
)

hasil_penjualan
```

Pengurutan membantu proses identifikasi kategori dengan performa tertinggi dan terendah.

---

## 4. Hasil Kegiatan

Setelah melakukan proses GroupBy dan Aggregation, data yang sebelumnya berupa kumpulan record dapat diringkas menjadi informasi berdasarkan kategori.

Hasil analisis dapat digunakan untuk mengetahui:

* Jumlah data pada setiap kategori.
* Total penjualan setiap kategori.
* Rata-rata penjualan setiap kategori.
* Nilai penjualan minimum dan maksimum.
* Kategori dengan performa penjualan tertinggi.
* Kategori dengan performa penjualan terendah.

Tahap ini membuat proses analisis menjadi lebih terarah karena data tidak hanya dilihat sebagai baris individual, tetapi juga sebagai kelompok yang dapat dibandingkan.

---

## 5. Insight yang Diperoleh

Dari praktik Week 8, terdapat beberapa pemahaman penting:

1. **GroupBy membantu mengubah data mentah menjadi ringkasan berdasarkan kelompok tertentu.**

2. **Aggregation memungkinkan data diringkas menggunakan statistik tertentu**, seperti total, rata-rata, jumlah data, nilai minimum, dan maksimum.

3. **Kombinasi GroupBy dan Aggregation sangat berguna dalam analisis bisnis**, terutama ketika ingin membandingkan performa antar kategori.

4. **Sorting membantu menemukan kelompok dengan nilai tertinggi maupun terendah** sehingga proses pencarian insight menjadi lebih cepat.

5. Hasil agregasi dapat menjadi dasar untuk analisis lanjutan dan pengambilan keputusan.

---

## 6. Kendala yang Ditemui

Beberapa hal yang perlu diperhatikan ketika menggunakan GroupBy dan Aggregation:

* Nama kolom harus ditulis dengan benar.
* Kolom yang digunakan untuk agregasi harus memiliki tipe data yang sesuai.
* Data kosong atau `NaN` perlu diperhatikan karena dapat memengaruhi hasil perhitungan.
* Pemilihan fungsi agregasi harus disesuaikan dengan tujuan analisis.
* Hasil agregasi perlu diinterpretasikan kembali dalam konteks bisnis dan tidak hanya dilihat sebagai angka.

---

## 7. Kesimpulan

Pada Week 8, telah dipelajari penggunaan **GroupBy dan Aggregation menggunakan Pandas** untuk mengelompokkan dan meringkas data.

Dengan menggunakan `groupby()`, data dapat dikelompokkan berdasarkan kategori tertentu. Selanjutnya, fungsi seperti `sum()`, `mean()`, `count()`, `min()`, `max()`, dan `.agg()` dapat digunakan untuk menghasilkan ringkasan statistik.

Kemampuan ini merupakan bagian penting dalam proses analisis data karena membantu seorang Data Analyst mengubah data mentah menjadi informasi yang lebih terstruktur dan dapat digunakan untuk menemukan pola serta mendukung pengambilan keputusan.

---

## 8. Dokumentasi

Dokumentasi yang perlu disimpan pada repository:

```text
Week_8_GroupBy_Aggregation/
│
├── Dataset/
│
├── Notebook/
│   └── Week_8_GroupBy_Aggregation.ipynb
│
├── Screenshot/
│   ├── 01_import_dataset.png
│   ├── 02_dataset_info.png
│   ├── 03_groupby.png
│   ├── 04_aggregation.png
│   ├── 05_multiple_aggregation.png
│   └── 06_sorted_result.png
│
└── Laporan_Week_8.md
```

---

## 9. Kompetensi yang Diperoleh

Setelah menyelesaikan kegiatan Week 8, kompetensi yang diperoleh meliputi:

* Memahami konsep `groupby()` pada Pandas.
* Melakukan pengelompokan data berdasarkan kategori.
* Menggunakan fungsi aggregation pada dataset.
* Menggunakan beberapa fungsi statistik secara bersamaan.
* Mengurutkan hasil analisis.
* Membaca dan menginterpretasikan hasil agregasi.
* Menghubungkan hasil pengolahan data dengan kebutuhan analisis bisnis.

---

**Status:** Selesai
**Tanggal:** 8 September 2026
