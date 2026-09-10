# WEEK 8 — BUSINESS QUESTION & PROBLEM SOLVING

**Nama:** Maulana Aldi Pradana
**Program:** Simulasi Industri Junior Data Analyst
**Topik:** Topik 5 – Problem Solving & Business Question
**Periode:** 7–11 September 2026
**Dataset:** `Final Clean Dataset.csv`
**Jumlah Data:** 10.000 baris × 10 kolom

---

## 1. Tujuan Kegiatan

Pada Week 8, kegiatan difokuskan pada pemahaman masalah bisnis dan penyusunan pertanyaan bisnis yang dapat dijawab menggunakan data.

Tujuan kegiatan adalah:

1. Memahami dan mendefinisikan business problem.
2. Menentukan konteks dan dampak bisnis dari permasalahan.
3. Mengidentifikasi stakeholder yang berkepentingan terhadap hasil analisis.
4. Menentukan informasi dan data yang dibutuhkan.
5. Menyusun business question dan sub question.
6. Menentukan KPI dan metrics yang relevan.
7. Melakukan root cause analysis.
8. Mengidentifikasi permasalahan berdasarkan hasil eksplorasi dataset.
9. Menyusun evidence, insight, dan problem tree sebagai dasar analisis lebih lanjut.

---

# 2. Dataset

Dataset yang digunakan adalah:

`Final Clean Dataset.csv`

Dataset terdiri dari **10.000 baris dan 10 kolom**, yaitu:

| No | Kolom            |
| -- | ---------------- |
| 1  | Transaction_ID   |
| 2  | Item             |
| 3  | Quantity         |
| 4  | Price_Per_Unit   |
| 5  | Total_Spent      |
| 6  | Payment_Method   |
| 7  | Location         |
| 8  | Transaction_Date |
| 9  | Year             |
| 10 | Month            |

### Hasil pemeriksaan awal

Ditemukan beberapa kondisi kualitas data:

* Missing `Transaction_Date`: **460 data (4,60%)**
* `Item` dengan nilai `UNKNOWN/ERROR`: **636 data (6,36%)**
* `Location` dengan nilai `UNKNOWN/ERROR`: **696 data (6,96%)**
* `Payment_Method` dengan nilai `UNKNOWN/ERROR`: **599 data (5,99%)**
* Sales mismatch antara `Total_Spent` dan `Quantity × Price_Per_Unit`: **1.194 data (11,94%)**
* Duplicate data: **0**

Temuan tersebut dicatat sebagai bagian dari data quality consideration dalam proses analisis.

---

# 3. Day 1 — Understand Business Problem

**Tanggal: 1 September 2026**

## 3.1 Business Problem

Permasalahan awal yang diberikan adalah bahwa penjualan perusahaan mengalami penurunan pada periode tertentu.

Setelah dilakukan pemeriksaan terhadap dataset, permasalahan dirumuskan secara lebih hati-hati menjadi:

> **Performa penjualan berfluktuasi dan belum stabil, dengan Februari 2023 sebagai periode sales terendah.**

Rumusan tersebut digunakan karena data menunjukkan adanya kenaikan dan penurunan sales antarperiode, bukan penurunan secara terus-menerus selama tiga bulan.

## 3.2 Business Context

Analisis dilakukan untuk memahami perubahan performa penjualan berdasarkan:

* waktu,
* produk,
* lokasi transaksi,
* metode pembayaran,
* jumlah transaksi,
* jumlah produk terjual.

Analisis tersebut diperlukan agar perubahan sales dapat dipahami berdasarkan evidence dari data.

## 3.3 Business Impact

Permasalahan penjualan yang berfluktuasi dapat berdampak pada:

* ketidakstabilan performa penjualan,
* kesulitan dalam melakukan perencanaan penjualan,
* kesulitan menentukan prioritas produk,
* ketergantungan terhadap segmen tertentu,
* serta risiko pengambilan keputusan berdasarkan data yang belum sepenuhnya valid.

## 3.4 Stakeholders

Stakeholder yang relevan:

1. **Owner / Management**
   Membutuhkan informasi mengenai kondisi dan arah performa penjualan.

2. **Sales / Marketing**
   Membutuhkan informasi mengenai produk dan periode yang memiliki performa berbeda.

3. **Operations**
   Membutuhkan informasi mengenai lokasi transaksi dan pola transaksi.

4. **Finance**
   Membutuhkan data transaksi yang valid untuk mendukung analisis penjualan.

5. **Data Analyst**
   Bertugas melakukan analisis, menemukan evidence, dan menyusun insight.

## 3.5 Data yang Dibutuhkan

Data yang dibutuhkan meliputi:

* Transaction ID
* Item
* Quantity
* Price per Unit
* Total Spent
* Payment Method
* Location
* Transaction Date
* Year
* Month

---

# 4. Day 2 — Business Question

**Tanggal: 2 September 2026**

Berdasarkan business problem, disusun lima business questions.

### BQ1 — Trend Penjualan

**Bagaimana tren penjualan berdasarkan waktu dan pada periode mana terjadi perubahan atau penurunan penjualan yang signifikan?**

Sub questions:

1. Bagaimana sales setiap bulan?
2. Bulan mana yang memiliki sales tertinggi?
3. Bulan mana yang memiliki sales terendah?
4. Pada bulan mana terjadi penurunan sales terbesar?
5. Apakah perubahan sales diikuti perubahan jumlah transaksi?

### BQ2 — Performa Produk

**Produk apa yang memberikan kontribusi terbesar dan produk apa yang memiliki performa penjualan paling rendah?**

Sub questions:

1. Produk apa yang menghasilkan sales terbesar?
2. Berapa kontribusi masing-masing produk?
3. Produk apa yang memiliki quantity terjual paling tinggi?
4. Produk apa yang memiliki jumlah transaksi paling tinggi?
5. Bagaimana performa produk pada periode dengan sales terendah?

### BQ3 — Performa Lokasi

**Bagaimana performa penjualan berdasarkan lokasi transaksi dan apakah terdapat lokasi dengan kontribusi penjualan yang rendah?**

Sub questions:

1. Lokasi mana yang menghasilkan sales terbesar?
2. Berapa kontribusi masing-masing lokasi?
3. Bagaimana jumlah transaksi setiap lokasi?
4. Bagaimana quantity berdasarkan lokasi?
5. Bagaimana performa lokasi pada periode sales terendah?

### BQ4 — Metode Pembayaran

**Bagaimana pola penjualan berdasarkan metode pembayaran dan apakah terdapat metode pembayaran dengan kontribusi transaksi atau nilai penjualan yang rendah?**

Sub questions:

1. Metode pembayaran apa yang paling banyak digunakan?
2. Berapa kontribusi sales setiap metode pembayaran?
3. Bagaimana jumlah transaksi berdasarkan metode pembayaran?
4. Bagaimana quantity berdasarkan metode pembayaran?
5. Bagaimana performa metode pembayaran pada periode sales terendah?

### BQ5 — Volume Transaksi

**Apakah perubahan penjualan berkaitan dengan perubahan jumlah transaksi dan jumlah produk yang terjual?**

Sub questions:

1. Apakah sales meningkat ketika jumlah orders meningkat?
2. Apakah sales menurun ketika quantity menurun?
3. Bagaimana hubungan sales dengan orders?
4. Bagaimana hubungan sales dengan quantity?
5. Apakah perubahan AOV berpengaruh terhadap perubahan sales?

---

# 5. Day 3 — KPI & Metrics

**Tanggal: 3 September 2026**

KPI digunakan untuk mengukur performa penjualan dan membantu menjawab business questions.

## 5.1 KPI yang Digunakan

| KPI / Metric          | Definisi                         | Formula                                | Tujuan                               |
| --------------------- | -------------------------------- | -------------------------------------- | ------------------------------------ |
| Total Sales           | Total nilai penjualan            | Σ Total_Spent                          | Mengukur nilai penjualan keseluruhan |
| AOV                   | Rata-rata nilai transaksi        | Total Sales / Orders                   | Mengukur rata-rata nilai transaksi   |
| Number of Orders      | Jumlah transaksi                 | COUNT(Transaction_ID)                  | Mengukur volume transaksi            |
| Total Quantity Sold   | Jumlah produk terjual            | Σ Quantity                             | Mengukur volume produk               |
| Sales Growth Rate     | Perubahan sales antarperiode     | (Current - Previous) / Previous × 100% | Mengukur pertumbuhan/penurunan sales |
| Product Contribution  | Kontribusi produk terhadap sales | Product Sales / Total Sales × 100%     | Mengetahui produk utama              |
| Location Contribution | Kontribusi lokasi terhadap sales | Location Sales / Total Sales × 100%    | Mengetahui ketergantungan lokasi     |

## 5.2 KPI Utama Dataset

Hasil perhitungan:

* **Total Sales:** 88.779,50
* **AOV:** 8,88
* **Number of Orders:** 10.000
* **Total Quantity Sold:** 30.271
* **Latest Sales Growth Rate:** +3,09%

## 5.3 Monthly Sales

| Bulan     |    Sales | Growth |
| --------- | -------: | -----: |
| Januari   | 7.221,00 |      — |
| Februari  | 6.584,00 | -8,82% |
| Maret     | 7.198,00 | +9,33% |
| April     | 7.138,50 | -0,83% |
| Mei       | 6.970,00 | -2,36% |
| Juni      | 7.327,50 | +5,13% |
| Juli      | 6.910,00 | -5,70% |
| Agustus   | 7.112,00 | +2,92% |
| September | 6.829,50 | -3,97% |
| Oktober   | 7.336,50 | +7,42% |
| November  | 6.884,50 | -6,16% |
| Desember  | 7.097,00 | +3,09% |

Dari data tersebut terlihat bahwa sales mengalami **fluktuasi antarbulan**.

---

# 6. Day 4 — Root Cause Analysis

**Tanggal: 4 September 2026**

Root Cause Analysis dilakukan menggunakan pendekatan:

* 5 Why
* Fishbone
* Pareto
* Drill Down

## 6.1 Permasalahan Utama

> **Performa penjualan berfluktuasi dan belum stabil, dengan Februari 2023 sebagai periode sales terendah.**

Februari 2023 memiliki:

* Sales: **6.584,00**
* Orders: **727**
* Quantity: **2.248**
* Sales Growth: **-8,82%**

Februari menjadi periode dengan sales terendah sekaligus mengalami penurunan terbesar dibandingkan bulan sebelumnya.

## 6.2 Product Analysis

Produk dengan kontribusi sales terbesar secara keseluruhan:

| Product  |     Sales | Contribution |
| -------- | --------: | -----------: |
| SALAD    | 17.021,00 |       19,17% |
| SANDWICH | 13.484,00 |       15,19% |
| JUICE    | 13.449,00 |       15,15% |
| SMOOTHIE | 13.132,00 |       14,79% |
| CAKE     | 10.341,00 |       11,65% |

SALAD menjadi produk dengan kontribusi sales terbesar.

## 6.3 Location Analysis

| Location |     Sales | Contribution |
| -------- | --------: | -----------: |
| TAKEAWAY | 55.645,00 |       62,68% |
| IN-STORE | 27.090,00 |       30,51% |
| ERROR    |  3.260,50 |        3,67% |
| UNKNOWN  |  2.784,00 |        3,14% |

Sales sangat terkonsentrasi pada lokasi **TAKEAWAY**, dengan kontribusi sebesar 62,68%.

## 6.4 Payment Analysis

| Payment Method |     Sales | Contribution |
| -------------- | --------: | -----------: |
| DIGITAL WALLET | 42.948,00 |       48,38% |
| CREDIT CARD    | 20.415,00 |       23,00% |
| CASH           | 20.334,00 |       22,90% |
| ERROR          |  2.621,50 |        2,95% |
| UNKNOWN        |  2.461,00 |        2,77% |

Metode pembayaran dengan kontribusi terbesar adalah **DIGITAL WALLET**, sebesar 48,38%.

## 6.5 Root Cause Candidates

Berdasarkan analisis, ditemukan beberapa kandidat penyebab:

### RC1 — Perubahan Volume Transaksi

Perubahan jumlah orders dan quantity antarperiode dapat berkontribusi terhadap perubahan sales.

### RC2 — Ketimpangan Kontribusi Produk

Kontribusi sales tidak tersebar secara merata sehingga perubahan performa produk utama dapat memengaruhi total sales.

### RC3 — Ketergantungan pada Lokasi Tertentu

TAKEAWAY memberikan kontribusi terbesar sehingga performa penjualan cukup terkonsentrasi pada segmen tersebut.

### RC4 — Perbedaan Kontribusi Payment Method

DIGITAL WALLET menjadi metode pembayaran dengan kontribusi terbesar sehingga distribusi transaksi tidak merata antarmetode pembayaran.

### RC5 — Kualitas Data

Data memiliki missing values, nilai UNKNOWN/ERROR, dan sales mismatch yang dapat memengaruhi reliability hasil analisis.

**Catatan:** kandidat root cause di atas merupakan hipotesis berdasarkan evidence dataset, bukan bukti hubungan sebab-akibat secara langsung.

---

# 7. Day 5 — Problem Analysis

**Tanggal: 5 September 2026**

Pada hari terakhir Week 8 dilakukan analisis terhadap dataset hasil cleaning dan eksplorasi untuk mengidentifikasi masalah, potential causes, evidence, dan insight.

## 7.1 Identifikasi Masalah

### P1 — Penjualan Mengalami Fluktuasi

Sales berubah naik dan turun antarbulan.

Bukti utama:

* Februari mengalami penurunan sebesar **-8,82%**.
* Terdapat beberapa bulan lain yang juga mengalami negative growth.

### P2 — Kontribusi Penjualan Terkonsentrasi pada Segmen Tertentu

Distribusi sales tidak merata.

Bukti utama:

* TAKEAWAY memberikan kontribusi **62,68%**.
* SALAD menjadi produk dengan kontribusi terbesar sebesar **19,17%**.
* DIGITAL WALLET memberikan kontribusi **48,38%**.

### P3 — Kualitas Data Masih Memiliki Ketidaksesuaian

Dataset masih memiliki beberapa masalah kualitas data.

Bukti utama:

* Missing Transaction Date: **460**
* Item UNKNOWN/ERROR: **636**
* Location UNKNOWN/ERROR: **696**
* Payment UNKNOWN/ERROR: **599**
* Sales mismatch: **1.194 (11,94%)**

---

# 8. Potential Causes

Potential causes yang diidentifikasi:

| Kode | Potential Cause                                  | Permasalahan Terkait |
| ---- | ------------------------------------------------ | -------------------- |
| C1   | Perubahan performa transaksi antarperiode        | P1                   |
| C2   | Perbedaan kontribusi produk terhadap total sales | P1, P2               |
| C3   | Ketergantungan pada lokasi transaksi tertentu    | P2                   |
| C4   | Perbedaan kontribusi metode pembayaran           | P2                   |
| C5   | Ketidakkonsistenan kualitas data transaksi       | P3                   |

---

# 9. Data Evidence

Evidence utama yang ditemukan:

| Kode | Evidence                                                                             |
| ---- | ------------------------------------------------------------------------------------ |
| E1   | Februari 2023 memiliki sales terendah sebesar 6.584,00                               |
| E2   | Februari 2023 mengalami sales decline terbesar sebesar -8,82%                        |
| E3   | SALAD memiliki kontribusi sales terbesar sebesar 19,17%                              |
| E4   | TAKEAWAY memiliki kontribusi sales terbesar berdasarkan lokasi sebesar 62,68%        |
| E5   | DIGITAL WALLET memiliki kontribusi sales terbesar berdasarkan payment sebesar 48,38% |
| E6   | Terdapat 460 transaksi dengan tanggal yang missing                                   |
| E7   | Terdapat 636 nilai Item UNKNOWN/ERROR                                                |
| E8   | Terdapat 696 nilai Location UNKNOWN/ERROR                                            |
| E9   | Terdapat 1.194 transaksi dengan sales mismatch atau 11,94%                           |

---

# 10. Business Insights

Berdasarkan hasil analisis, diperoleh tiga insight utama.

## Insight 1 — Masalah Utama adalah Fluktuasi, Bukan Penurunan Terus-Menerus

Data menunjukkan bahwa penjualan tidak mengalami penurunan secara terus-menerus selama tiga bulan.

Sebaliknya, sales mengalami pola naik-turun antarbulan.

Februari merupakan periode terlemah dengan sales **6.584,00** dan growth **-8,82%**.

## Insight 2 — Sales Terkonsentrasi pada Produk dan Segmen Tertentu

Kontribusi sales tidak tersebar secara merata.

SALAD merupakan produk dengan kontribusi terbesar, sedangkan TAKEAWAY mendominasi kontribusi berdasarkan lokasi.

Hal tersebut menunjukkan adanya konsentrasi sales pada segmen tertentu yang perlu diperhatikan dalam pengambilan keputusan.

## Insight 3 — Data Quality Perlu Menjadi Perhatian

Terdapat **1.194 transaksi atau 11,94%** yang memiliki perbedaan antara `Total_Spent` dan hasil perhitungan `Quantity × Price_Per_Unit`.

Selain itu masih terdapat missing date dan nilai UNKNOWN/ERROR.

Oleh karena itu, data quality perlu diperhatikan agar analisis dan keputusan bisnis berikutnya lebih reliable.

---

# 11. Problem Tree

Problem Tree yang dibuat pada Week 8 memiliki struktur:

```text
                         MAIN PROBLEM
                              │
          Performa penjualan berfluktuasi dan belum stabil
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
   Volume Transaksi      Distribusi Sales       Data Quality
        │                     │                     │
   Orders berubah        Produk tidak merata    Missing Date
   Quantity berubah      Lokasi terkonsentrasi   UNKNOWN/ERROR
                         Payment terkonsentrasi   Sales mismatch
        │                     │                     │
        └─────────────────────┼─────────────────────┘
                              │
                         BUSINESS IMPACT
                              │
                Sulit menjaga stabilitas sales
                dan mengambil keputusan secara
                       konsisten berbasis data
```

---

# 12. Output Week 8

Seluruh output Week 8 berhasil dibuat:

```text
Week_8_Business_Question/
│
├── Business Problem Statement.pdf
├── Business Question.xlsx
├── KPI Definition.xlsx
├── Root Cause Analysis.pdf
├── Problem Tree.pdf
└── Analysis Notebook.ipynb
```

## Ringkasan Output

| Output                         | Status    |
| ------------------------------ | --------- |
| Business Problem Statement.pdf | ✅ Selesai |
| Business Question.xlsx         | ✅ Selesai |
| KPI Definition.xlsx            | ✅ Selesai |
| Root Cause Analysis.pdf        | ✅ Selesai |
| Problem Tree.pdf               | ✅ Selesai |
| Analysis Notebook.ipynb        | ✅ Selesai |

---

# 13. Kesimpulan

Week 8 berhasil menyelesaikan tahapan **Business Question & Problem Solving** menggunakan dataset `Final Clean Dataset.csv`.

Analisis menunjukkan bahwa permasalahan utama bukan berupa penurunan sales secara terus-menerus, melainkan **fluktuasi penjualan yang belum stabil**, dengan **Februari 2023** sebagai periode sales terendah.

Pada Februari 2023:

* Sales sebesar **6.584,00**
* Orders sebanyak **727**
* Quantity sebanyak **2.248**
* Sales mengalami perubahan **-8,82%**
* Orders mengalami perubahan **-11,12%**
* Quantity mengalami perubahan **-8,73%**

Analisis juga menunjukkan bahwa sales terkonsentrasi pada beberapa segmen, terutama:

* **SALAD:** kontribusi 19,17% secara keseluruhan.
* **TAKEAWAY:** kontribusi 62,68%.
* **DIGITAL WALLET:** kontribusi 48,38%.

Selain itu, kualitas data masih perlu diperhatikan karena terdapat **1.194 transaksi (11,94%) dengan sales mismatch**, serta beberapa missing value dan nilai UNKNOWN/ERROR.

Hasil Week 8 kemudian menjadi dasar untuk memasuki **Week 9 – Problem Solving**, khususnya tahap Root Cause Analysis Lanjutan, Solution Analysis, Data-driven Recommendation, Stakeholder Consultation, dan Final Business Case.
