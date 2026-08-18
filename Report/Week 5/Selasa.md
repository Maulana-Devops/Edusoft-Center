# 📊 Topik 3: Data Cleaning & Preparation — Cafe Sales Dataset

Dokumentasi ini berisi catatan proses dan *deliverables* dari simulasi pembersihan dan penyiapan data (*Data Cleaning & Preparation*) untuk dataset transaksi **Cafe Sales** dari **Day 1 hingga Day 4**.

---

## 📑 Daftar Isi
- [Ringkasan Proyek](#-ringkasan-proyek)
- [Day 1: Initial Data Audit](#-day-1-initial-data-audit)
- [Day 2: Handling Missing Values & Duplicates](#-day-2-handling-missing-values--duplicates)
- [Day 3: Data Standardization](#-day-3-data-standardization)
- [Day 4: Feature Engineering & Final Dataset](#-day-4-feature-engineering--final-dataset)
- [Struktur Repositori](#-struktur-repositori)

---

## 📌 Ringkasan Proyek

| Item | Keterangan |
| :--- | :--- |
| **Dataset Raw** | `dirty_cafe_sales.csv` (10.000 baris × 8 kolom) |
| **Bahasa / Library** | Python (`pandas`, `numpy`, `openpyxl`) |
| **Output Akhir** | `Final Clean Dataset.csv` & Laporan Excel (Day 1–4) |

---

## 📅 Day 1: Initial Data Audit

### 🎯 Tujuan
Melakukan pemeriksaan awal (*health check*) terhadap *raw dataset* untuk mengidentifikasi isu kualitas data tanpa mengubah isi data.

### 🔍 Ringkasan Hasil Audit
* **Jumlah Data:** 10.000 baris, 8 kolom.
* **Duplikat:** `0` baris duplikat terdeteksi.
* **Tipe Data Anomalik:** Kolom numerik (`Quantity`, `Price Per Unit`, `Total Spent`) dan tanggal (`Transaction Date`) tersimpan sebagai tipe `object` (string) akibat adanya karakter *noise*.
* **Missing Values:**
  * `Item`: 333
  * `Quantity`: 138
  * `Price Per Unit`: 179
  * `Total Spent`: 173
  * `Payment Method`: 2.579
  * `Location`: 3.265
  * `Transaction Date`: 159

### 📦 Deliverables Day 1
- `Initial Data Audit.xlsx`

---

## 📅 Day 2: Handling Missing Values & Duplicates

### 🎯 Tujuan
Membersihkan data hilang (*missing values*) dan memastikan dataset bebas dari duplikasi.

### 🛠️ Strategi Pembersihan
1. **Pembersihan Karakter Non-Angka:** Menghapus *noise* karakter string dari kolom numerik.
2. **Imputasi Data Numerik:** Memakai nilai **Median** untuk kolom `Quantity`, `Price Per Unit`, dan `Total Spent`.
3. **Imputasi Data Kategorikal/Tanggal:** Memakai nilai **Modus (Mode)** untuk kolom `Item`, `Payment Method`, `Location`, dan `Transaction Date`.
4. **Validasi Duplikat:** Memastikan `0` baris duplikat.

### 📋 Ringkasan Hasil Pembersihan

| Nama Kolom | Jumlah Missing (Sebelum) | Strategi Imputasi | Nilai Imputasi | Jumlah Missing (Sesudah) |
| :--- | :---: | :--- | :---: | :---: |
| `Item` | 333 | Modus | `COFFEE` | 0 |
| `Quantity` | 138 | Median | `2.0` | 0 |
| `Price Per Unit` | 179 | Median | `2.0` | 0 |
| `Total Spent` | 173 | Median | `4.0` | 0 |
| `Payment Method` | 2.579 | Modus | `CASH` | 0 |
| `Location` | 3.265 | Modus | `IN-STORE` | 0 |
| `Transaction Date` | 159 | Modus | `2023-09-08` | 0 |

### 📦 Deliverables Day 2
- `Clean Dataset v1.csv`
- `Data Cleaning Log.xlsx`

---

## 📅 Day 3: Data Standardization

### 🎯 Tujuan
Menyeragamkan penamaan kolom, nilai string/teks, dan format tanggal sesuai standar industri.

### 🛠️ Aturan Standardisasi
1. **Nama Kolom:** Format `Title_Case` dengan pemisah *underscore* (`_`).
2. **Nilai Teks:** Seluruh nilai kategorikal diubah menjadi **`UPPERCASE`**.
3. **Format Tanggal:** Konversi ke standar ISO 8601 (`YYYY-MM-DD`).

### 📋 Ringkasan Perubahan Format

| Elemen Dataset | Sebelum Standardisasi | Sesudah Standardisasi | Aturan Standardisasi |
| :--- | :--- | :--- | :--- |
| **Nama Kolom** | `Transaction ID`, `Price Per Unit` | `Transaction_ID`, `Price_Per_Unit` | Title_Case dengan Underscore |
| **Nilai Teks** | `Coffee`, `Credit Card`, `Takeaway` | `COFFEE`, `CREDIT CARD`, `TAKEAWAY` | Upper Case (`UPPERCASE`) |
| **Tanggal** | String bervariasi | `2023-09-08` | ISO Format (`YYYY-MM-DD`) |

### 📦 Deliverables Day 3
- `Clean Dataset v2.csv`
- `Data Standardization Report.xlsx`

---

## 📅 Day 4: Feature Engineering & Final Dataset

### 🎯 Tujuan
Merekayasa fitur/kolom baru dari data yang ada untuk mendukung kebutuhan analisis bisnis lanjutan (EDA/BI Dashboard).

### 💡 Fitur Baru yang Dibuat

| Nama Kolom Baru | Formula / Sumber Data | Tipe Data | Tujuan & Relevansi Analisis |
| :--- | :--- | :--- | :--- |
| **`Year`** | `Year(Transaction_Date)` | Integer | Mengelompokkan dan menganalisis tren pertumbuhan tahunan |
| **`Month`** | `Month_Name(Transaction_Date)` | String | Menganalisis pola transaksi & fluktuasi penjualan bulanan (*seasonality*) |

### 📦 Deliverables Day 4
- `Final Clean Dataset.csv`
- `Feature Engineering Documentation.xlsx`

---

## 📂 Struktur Repositori

```text
.
├── README.md
├── datasets/
│   ├── dirty_cafe_sales.csv
│   ├── Clean Dataset v1.csv
│   ├── Clean Dataset v2.csv
│   └── Final Clean Dataset.csv
├── notebooks/
│   └── Data_Cleaning_and_Preparation.ipynb
└── reports/
    ├── Initial Data Audit.xlsx
    ├── Data Cleaning Log.xlsx
    ├── Data Standardization Report.xlsx
    └── Feature Engineering Documentation.xlsx
