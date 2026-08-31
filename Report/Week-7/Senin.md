
# Laporan PKL — Week 7

## Menghitung Korelasi Antar Kolom di Pandas untuk Menemukan Hubungan Data

### 📅 Pelaksanaan
31 Agustus 2026 — Week 7

### 🎯 Tujuan Pembelajaran


Pada minggu ketujuh, kegiatan difokuskan pada pemahaman korelasi dalam analisis data. Korelasi digunakan untuk melihat arah dan kekuatan hubungan antara dua variabel atau lebih.

Tujuan kegiatan minggu ini adalah:

- Memahami konsep dasar korelasi.
- Mengetahui fungsi korelasi dalam Data Analysis.
- Menghitung korelasi antar kolom menggunakan Pandas.
- Memahami cara membaca nilai koefisien korelasi.
- Membandingkan hubungan antarvariabel.
- Memvisualisasikan matriks korelasi menggunakan heatmap.
- Belajar menulis insight berdasarkan hasil analisis.
- Memahami bahwa korelasi tidak selalu menunjukkan hubungan sebab-akibat.

---

## 📚 Materi yang Dipelajari

Materi yang dipelajari pada Week 7 meliputi:

1. Pengertian korelasi.
2. Koefisien korelasi dengan rentang -1 hingga +1.
3. Korelasi positif dan negatif.
4. Korelasi yang mendekati nol.
5. Fungsi `corr()` pada Pandas.
6. Parameter `numeric_only=True`.
7. Matriks korelasi.
8. Visualisasi korelasi menggunakan heatmap.
9. Interpretasi hasil korelasi.
10. Perbedaan korelasi dan sebab-akibat.

---

## 🛠️ Tools yang Digunakan

- Google Colab
- Python
- Pandas
- Matplotlib
- Seaborn

---

## 🧪 Praktik yang Dilakukan

### 1. Membuat Dataset

Saya membuat dataset sederhana yang berisi informasi mengenai:

- Jam belajar
- Kehadiran
- Nilai siswa

Dataset tersebut digunakan sebagai bahan latihan untuk mengetahui hubungan antarvariabel.

Contoh struktur data:

```python
import pandas as pd

data = pd.DataFrame({
    "Jam_Belajar": [1, 2, 2, 3, 3, 4, 4, 5, 5, 6],
    "Kehadiran": [70, 75, 78, 80, 82, 85, 88, 90, 92, 95],
    "Nilai": [55, 60, 64, 68, 72, 76, 79, 84, 87, 91]
})

print(data)
````

### 2. Memeriksa Struktur Dataset

Sebelum melakukan perhitungan, dataset diperiksa terlebih dahulu menggunakan fungsi `info()` dan `describe()`.

```python
print(data.info())
print(data.describe())
```

Tahap ini dilakukan untuk memastikan struktur dan tipe data sudah sesuai sebelum digunakan dalam analisis.

### 3. Menghitung Korelasi

Perhitungan korelasi dilakukan menggunakan fungsi `corr()` pada Pandas.

```python
korelasi = data.corr(numeric_only=True)

print(korelasi)
```

Hasilnya berupa matriks yang menunjukkan nilai korelasi antar kolom numerik.

### 4. Membuat Heatmap

Untuk mempermudah pembacaan matriks korelasi, hasilnya divisualisasikan menggunakan heatmap.

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.heatmap(
    data.corr(numeric_only=True),
    annot=True,
    cmap="coolwarm"
)

plt.title("Matriks Korelasi")
plt.show()
```

Heatmap membantu melihat pola hubungan antarvariabel secara visual.

---

## 🔎 Studi Kasus

Studi kasus yang digunakan adalah hubungan antara jam belajar, kehadiran, dan nilai siswa.

Pertanyaan yang ingin dijawab:

> Variabel apa yang memiliki hubungan paling kuat dengan nilai siswa?

Melalui perhitungan korelasi, hubungan antarvariabel dapat dibandingkan dalam bentuk angka.

Contohnya, jika korelasi antara `Jam_Belajar` dan `Nilai` mendekati +1, maka terdapat hubungan linear positif yang kuat pada dataset tersebut.

Namun, hasil tersebut tidak dapat langsung digunakan untuk menyimpulkan bahwa jam belajar merupakan satu-satunya penyebab meningkatnya nilai.

---

## 💡 Insight yang Dipelajari

Dari praktik yang dilakukan, saya memahami bahwa korelasi dapat digunakan sebagai langkah awal untuk menemukan pola dalam dataset.

Beberapa hal yang dipelajari:

* Nilai korelasi positif menunjukkan kecenderungan dua variabel bergerak ke arah yang sama.
* Nilai korelasi negatif menunjukkan kecenderungan dua variabel bergerak ke arah berlawanan.
* Nilai yang mendekati nol menunjukkan hubungan linear yang lemah atau tidak jelas.
* Korelasi tidak dapat langsung digunakan untuk membuktikan hubungan sebab-akibat.
* Hasil korelasi perlu dipahami bersama konteks dan kondisi dataset.

---

## ⚠️ Kendala yang Ditemui

Beberapa hal yang perlu diperhatikan selama praktik:

1. Hasil korelasi dapat sulit dipahami jika jumlah variabel cukup banyak.
2. Nilai korelasi yang tinggi dapat disalahartikan sebagai hubungan sebab-akibat.
3. Data yang belum diperiksa dapat menghasilkan interpretasi yang kurang tepat.
4. Membaca matriks korelasi secara manual menjadi kurang praktis ketika jumlah kolom bertambah.

---

## 🔧 Solusi

Untuk mengatasi kendala tersebut:

* Melakukan pemeriksaan dataset sebelum menghitung korelasi.
* Menggunakan `numeric_only=True` untuk membatasi perhitungan pada kolom numerik.
* Menggunakan heatmap agar matriks korelasi lebih mudah dibaca.
* Membandingkan hasil korelasi dengan visualisasi seperti scatter plot.
* Tidak membuat kesimpulan sebab-akibat hanya berdasarkan nilai korelasi.

---

## 📸 Dokumentasi Praktik

Dokumentasi yang disiapkan untuk artikel:

* [ ] Screenshot dataset pada Google Colab
* [ ] Screenshot hasil `info()` atau `describe()`
* [ ] Screenshot perhitungan `corr()`
* [ ] Screenshot kode pembuatan heatmap
* [ ] Screenshot hasil heatmap
* [ ] Screenshot mini praktik

---

## 📝 Hasil Pembelajaran

Setelah menyelesaikan kegiatan Week 7, saya dapat:

* Menjelaskan konsep dasar korelasi.
* Menghitung korelasi menggunakan Pandas.
* Membaca matriks korelasi.
* Membandingkan hubungan antarvariabel.
* Membuat visualisasi heatmap.
* Menjelaskan hasil korelasi dengan lebih hati-hati.
* Membedakan antara korelasi dan hubungan sebab-akibat.

---

## 🌐 Hasil Dokumentasi

Materi yang dipelajari kemudian didokumentasikan dalam bentuk artikel blog Edusoft dengan judul:

> Menghitung Korelasi Antar Kolom di Pandas untuk Menemukan Hubungan Data

Artikel tersebut dilengkapi dengan contoh kode Python, hasil praktik, screenshot dokumentasi, serta penjelasan mengenai interpretasi korelasi.

---

## 📌 Kesimpulan

Week 7 menjadi lanjutan dari pembelajaran mengenai visualisasi hubungan antarvariabel pada minggu sebelumnya.

Jika pada Week 6 hubungan data dilihat menggunakan scatter plot, pada Week 7 hubungan tersebut mulai diukur secara numerik menggunakan korelasi.

Melalui penggunaan Pandas, proses perhitungan korelasi dapat dilakukan dengan relatif sederhana. Namun, kemampuan teknis menjalankan `corr()` saja belum cukup. Hasil yang diperoleh tetap perlu diinterpretasikan dengan benar dan tidak boleh langsung dianggap sebagai hubungan sebab-akibat.

Pembelajaran ini menjadi dasar penting sebelum masuk ke tahap analisis data yang lebih kompleks pada minggu berikutnya.

````

### Struktur file GitHub

Kalau laporan mingguanmu disimpan per folder, saya sarankan:

```text
week-07/
├── README.md
└── dokumentasi/
    ├── 01-dataset.png
    ├── 02-info-dataset.png
    ├── 03-hasil-korelasi.png
    ├── 04-kode-heatmap.png
    ├── 05-hasil-heatmap.png
    └── 06-mini-praktik.png
````

Dengan pola ini, laporan GitHub Week 7 akan konsisten dengan Week 4–6 dan nantinya mudah dilanjutkan sampai Week 12.
