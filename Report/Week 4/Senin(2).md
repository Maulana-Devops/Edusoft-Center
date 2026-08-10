# Daily Report — Week 4

**Tanggal:** 10 Agustus 2026  
**Program:** PKL — Data Analysis  
**Minggu:** Week 4  
**Topik:** Data Cleaning dengan Pandas  
**Peserta:** Maulana Aldi Pradana

---

## 🎯 Tujuan Pembelajaran

Pada kegiatan hari ini, tujuan pembelajaran yang ingin dicapai adalah:

- Memahami konsep dasar Data Cleaning.
- Memahami pentingnya membersihkan dataset sebelum melakukan analisis.
- Mempelajari cara menangani masalah umum pada dataset menggunakan Pandas.
- Mempersiapkan artikel teknis sebagai dokumentasi hasil pembelajaran.
- Mengenal penerapan dasar SEO pada artikel blog.

---

## 📚 Materi yang Dipelajari

Materi utama yang dipelajari adalah **Data Cleaning**, yaitu proses memeriksa dan memperbaiki dataset agar lebih konsisten dan siap digunakan untuk analisis.

Beberapa permasalahan data yang dipelajari meliputi:

- Missing Value
- Data Duplikat
- Format Data yang Tidak Konsisten
- Tipe Data yang Tidak Sesuai
- Validasi Dataset Setelah Cleaning

Selain itu, dipelajari pula konsep **raw data** dan **clean data**, serta pentingnya menjaga dataset mentah agar tidak langsung dimodifikasi.

---

## 💻 Praktik yang Dilakukan

Praktik dilakukan menggunakan **Google Colab** dan **Pandas**.

Dataset sederhana dibuat menggunakan `pd.DataFrame()` untuk mensimulasikan data yang memiliki beberapa masalah.

Contoh:

```python
import pandas as pd

data = pd.DataFrame({
    "Nama": ["Andi", "Budi", "Andi", "Citra", "Doni"],
    "Umur": [20, None, 20, "21", 22],
    "Kota": ["Solo", "solo", "Solo", "Jogja", "Jogja"],
    "Nilai": [90, 85, 90, None, 88]
})

print(data)
