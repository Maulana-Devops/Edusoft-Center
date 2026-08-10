Data Cleaning dengan Pandas: Membersihkan Dataset dengan Python
📘 Apa yang Akan Dipelajari?

Pada artikel ini kamu akan mempelajari:

Memahami tujuan data cleaning dalam proses Data Analysis.
Memeriksa kondisi dataset sebelum melakukan pembersihan.
Menangani missing value atau data yang kosong.
Menghapus data yang terduplikasi.
Menstandarkan format data agar lebih konsisten.
Memperbaiki tipe data pada kolom tertentu.
Melakukan pemeriksaan ulang setelah proses data cleaning.
Mengenal praktik sederhana untuk menjaga data mentah tetap aman.
💡 Pendahuluan

Pada artikel sebelumnya, kita telah membahas bahwa dataset yang diperoleh dari berbagai sumber belum tentu langsung siap digunakan untuk analisis. Data dapat memiliki berbagai masalah, seperti nilai yang kosong, data yang terduplikasi, penulisan yang tidak konsisten, maupun tipe data yang tidak sesuai.

Menemukan masalah tersebut merupakan langkah awal. Setelah mengetahui kondisi dataset, langkah berikutnya adalah melakukan data cleaning, yaitu proses memeriksa dan memperbaiki data agar menjadi lebih konsisten dan siap digunakan untuk tahap analisis berikutnya.

Pada artikel ini, proses tersebut akan dilakukan secara langsung menggunakan Python dan Pandas. Dataset yang digunakan sengaja dibuat memiliki beberapa masalah agar setiap tahapan dapat terlihat dengan jelas.

⚠️ Sebelum Memulai

Sebelum mengikuti praktik pada artikel ini, pastikan kamu telah menyiapkan:

Akun Google.
Google Colab.
Pemahaman dasar Python.
Pemahaman dasar penggunaan Pandas.

Jika belum mengenal Google Colab, kamu dapat membaca artikel sebelumnya mengenai cara menjalankan Python tanpa melakukan instalasi pada komputer.

💻 Menyiapkan Dataset

Langkah pertama adalah membuat dataset sederhana menggunakan Pandas. Dataset ini akan digunakan sebagai contoh untuk melakukan proses data cleaning.

Jalankan kode berikut pada Google Colab:

import pandas as pd

data = pd.DataFrame({
    "Nama": ["Andi", "Budi", "Andi", "Citra", "Doni"],
    "Umur": [20, None, 20, "21", 22],
    "Kota": ["Solo", "solo", "Solo", "Jogja", "Jogja"],
    "Nilai": [90, 85, 90, None, 88]
})

print(data)

Kode tersebut membuat sebuah DataFrame dengan empat kolom, yaitu Nama, Umur, Kota, dan Nilai.

Jika kode berhasil dijalankan, akan muncul data seperti berikut:

    Nama        Umur   Kota  Nilai
0   Andi          20   Solo   90.0
1   Budi        None   solo   85.0
2   Andi          20   Solo   90.0
3  Citra          21  Jogja    NaN
4   Doni          22  Jogja   88.0

📸 Dokumentasi 1 — Dataset sebelum proses cleaning

Ambil screenshot Google Colab yang memperlihatkan kode dan hasil output tersebut.

Dataset tersebut sengaja dibuat memiliki beberapa masalah. Misalnya, terdapat nilai kosong pada kolom Umur dan Nilai, terdapat data Andi yang muncul dua kali, serta penulisan Solo dan solo yang belum konsisten.

🔍 Memeriksa Kondisi Dataset

Sebelum memperbaiki data, kita perlu mengetahui kondisi dataset terlebih dahulu. Jangan langsung menghapus atau mengubah data tanpa mengetahui masalah yang terdapat di dalamnya.

1. Memeriksa Struktur Dataset

Gunakan fungsi info():

data.info()

Fungsi info() memberikan informasi mengenai jumlah baris, jumlah kolom, jumlah data yang terisi, serta tipe data pada setiap kolom.

Contoh informasi yang dapat diperoleh:

RangeIndex: 5 entries, 0 to 4
Data columns (total 4 columns):
Nama
Umur
Kota
Nilai

Dari hasil tersebut kita dapat melihat apakah terdapat kolom dengan data yang belum lengkap atau tipe data yang perlu diperiksa lebih lanjut.

📸 Dokumentasi 2 — Memeriksa struktur dataset menggunakan info()

2. Memeriksa Missing Value

Selanjutnya kita dapat memeriksa jumlah data kosong pada setiap kolom.

Gunakan:

data.isnull().sum()

Contoh hasil:

Nama     0
Umur     1
Kota     0
Nilai    1
dtype: int64

Dari hasil tersebut dapat diketahui bahwa terdapat satu nilai kosong pada kolom Umur dan satu nilai kosong pada kolom Nilai.

Nilai kosong seperti None atau NaN disebut sebagai missing value. Jika tidak ditangani dengan tepat, keberadaan data kosong dapat memengaruhi proses analisis.

📸 Dokumentasi 3 — Memeriksa jumlah missing value

3. Memeriksa Data Duplikat

Masalah berikutnya adalah data yang muncul lebih dari satu kali.

Untuk memeriksanya, gunakan:

data.duplicated().sum()

Jika hasilnya:

1

berarti terdapat satu baris yang terduplikasi.

Pada dataset kita, data Andi muncul dua kali dengan informasi yang sama. Namun, sebelum menghapusnya, kita tetap perlu memastikan bahwa data tersebut memang merupakan duplikasi dan bukan dua transaksi atau kejadian yang berbeda.

🧹 Menangani Missing Value

Setelah mengetahui bahwa terdapat data kosong, kita dapat menentukan metode penanganannya.

Salah satu cara adalah mengisi nilai kosong menggunakan nilai rata-rata (mean). Contohnya pada kolom Nilai:

data["Nilai"] = data["Nilai"].fillna(data["Nilai"].mean())

Setelah menjalankan kode tersebut, nilai kosong pada kolom Nilai akan digantikan dengan nilai rata-rata dari data yang tersedia.

Untuk melihat hasilnya:

print(data)

📸 Dokumentasi 4 — Menangani missing value pada kolom Nilai

⚠️ Perlu Diperhatikan

Mengisi semua data kosong menggunakan rata-rata bukan berarti selalu menjadi pilihan terbaik. Metode yang digunakan harus disesuaikan dengan karakteristik data dan tujuan analisis.

Dalam beberapa kondisi, data kosong lebih tepat dihapus, diisi dengan median, menggunakan nilai tertentu, atau ditangani berdasarkan aturan bisnis.

🗑️ Menghapus Data Duplikat

Jika setelah diperiksa data tersebut memang merupakan duplikasi, kita dapat menggunakan fungsi drop_duplicates().

data = data.drop_duplicates()

Kemudian periksa kembali:

print(data)

Data yang identik akan dihapus sehingga setiap baris hanya muncul satu kali.

📸 Dokumentasi 5 — Menghapus data duplikat menggunakan drop_duplicates()

Namun, perlu diingat bahwa menghapus data bukan selalu solusi yang tepat. Data harus diperiksa terlebih dahulu agar informasi penting tidak ikut hilang.

🔤 Menstandarkan Format Data

Data yang memiliki nilai sama tetapi ditulis dengan format berbeda juga dapat menjadi masalah.

Contohnya:

Solo
solo
SOLO

Walaupun ketiganya merujuk pada kota yang sama, komputer dapat menganggapnya sebagai nilai yang berbeda.

Kita dapat menggunakan .str.title() untuk membuat penulisan menjadi lebih konsisten:

data["Kota"] = data["Kota"].str.title()

Kemudian periksa:

print(data["Kota"])

Hasilnya akan menjadi:

0     Solo
1     Solo
2     Solo
3    Jogja
4    Jogja

Dengan demikian, variasi penulisan solo telah diubah menjadi Solo.

📸 Dokumentasi 6 — Menstandarkan format nama kota

🔢 Memeriksa dan Memperbaiki Tipe Data

Selain nilai kosong dan data duplikat, tipe data juga perlu diperhatikan.

Gunakan:

print(data.dtypes)

Fungsi tersebut digunakan untuk melihat tipe data setiap kolom.

Jika terdapat kolom yang seharusnya berupa angka tetapi terbaca sebagai teks, kita dapat melakukan konversi menggunakan pd.to_numeric().

Contohnya:

data["Umur"] = pd.to_numeric(data["Umur"], errors="coerce")

Parameter errors="coerce" akan mengubah nilai yang tidak dapat dikonversi menjadi NaN. Hal ini perlu diperhatikan karena nilai yang berubah menjadi NaN nantinya harus ditangani kembali.

Setelah itu kita dapat memeriksa hasilnya:

print(data.dtypes)

📸 Dokumentasi 7 — Memeriksa tipe data setelah proses cleaning

✅ Memvalidasi Dataset Setelah Cleaning

Proses data cleaning tidak berhenti setelah kita menjalankan beberapa fungsi. Dataset perlu diperiksa kembali untuk memastikan perubahan yang dilakukan memberikan hasil yang sesuai.

Gunakan:

print(data.info())
print(data.isnull().sum())
print(data.duplicated().sum())

Dari pemeriksaan tersebut kita dapat mengetahui:

Apakah masih terdapat data kosong.
Apakah masih terdapat data duplikat.
Apakah struktur dataset sudah sesuai.
Apakah tipe data sudah sesuai dengan kebutuhan.

Tahap ini disebut validasi, yaitu proses memastikan bahwa data setelah dibersihkan berada dalam kondisi yang sesuai sebelum digunakan untuk analisis.

⭐ Best Practice: Jangan Mengubah Raw Data Secara Langsung

Salah satu kebiasaan yang baik dalam pengolahan data adalah menjaga dataset mentah tetap tersedia.

Daripada langsung mengubah data, kita dapat membuat salinan:

clean_data = data.copy()

Kemudian proses pembersihan dilakukan pada clean_data.

clean_data = clean_data.drop_duplicates()

Dengan cara tersebut, data awal masih dapat digunakan sebagai referensi apabila terjadi kesalahan selama proses pembersihan.

Secara sederhana, alurnya dapat digambarkan seperti berikut:

Raw Data
   ↓
Pemeriksaan
   ↓
Data Cleaning
   ↓
Validasi
   ↓
Clean Data
   ↓
Analisis
💼 Dalam Dunia Kerja

Dalam pekerjaan Data Analyst, data cleaning bukan sekadar menghapus data yang terlihat salah. Setiap perubahan terhadap dataset perlu memiliki alasan yang jelas.

Misalnya, ketika menemukan data kosong, seorang analis perlu mempertimbangkan apakah data tersebut harus dihapus, diisi dengan nilai tertentu, atau dibiarkan kosong. Begitu pula dengan data duplikat. Tidak semua data yang terlihat sama merupakan duplikasi karena bisa saja mewakili transaksi atau kejadian yang berbeda.

Karena itu, proses data cleaning membutuhkan kombinasi antara kemampuan teknis, pemahaman terhadap dataset, dan konteks bisnis.

❌ Kesalahan yang Sering Dilakukan Pemula

Beberapa kesalahan yang perlu dihindari ketika melakukan data cleaning antara lain:

Langsung menghapus semua baris yang memiliki data kosong.
Mengisi seluruh missing value menggunakan rata-rata tanpa mempertimbangkan konteks.
Menghapus data duplikat tanpa melakukan pemeriksaan terlebih dahulu.
Mengubah data mentah secara langsung tanpa membuat salinan.
Tidak melakukan validasi setelah proses cleaning.
Menganggap dataset sudah bersih hanya karena tidak menampilkan error ketika dijalankan.
🧪 Mini Challenge

Sekarang coba buat dataset sederhana berikut:

import pandas as pd

data = pd.DataFrame({
    "Nama": ["Rina", "Budi", "Rina", "Doni"],
    "Kota": ["solo", "Solo", "solo", "Jogja"],
    "Nilai": [85, None, 85, 90]
})

print(data)

Coba lakukan beberapa hal berikut:

Periksa jumlah missing value.
Periksa apakah terdapat data duplikat.
Standarkan penulisan nama kota.
Tangani nilai kosong pada kolom Nilai.
Periksa kembali kondisi dataset setelah dibersihkan.

Mini challenge ini dapat digunakan sebagai latihan untuk memastikan bahwa konsep yang telah dipelajari tidak hanya dipahami secara teori, tetapi juga dapat diterapkan secara langsung.

📖 Tahukah Kamu?

Dataset yang terlihat sederhana dapat memiliki berbagai masalah yang tidak langsung terlihat ketika pertama kali dibuka. Oleh karena itu, pemeriksaan awal sangat penting dalam proses Data Analysis.

Semakin besar dataset yang digunakan, semakin sulit melakukan pemeriksaan secara manual. Inilah salah satu alasan mengapa tools seperti Pandas banyak digunakan untuk membantu proses pengolahan data.

🎯 Kesimpulan

Data cleaning merupakan salah satu tahapan penting sebelum dataset digunakan untuk analisis. Proses ini tidak hanya berkaitan dengan menghapus data, tetapi juga mencakup pemeriksaan, penanganan nilai kosong, penghapusan duplikasi, standardisasi format, perbaikan tipe data, dan validasi hasil.

Dengan menggunakan Pandas, berbagai proses tersebut dapat dilakukan secara lebih sistematis dan efisien. Namun, fungsi yang tersedia tidak boleh digunakan secara sembarangan. Setiap perubahan terhadap data perlu mempertimbangkan konteks dan tujuan analisis.

Setelah dataset memiliki kualitas yang lebih baik, tahap berikutnya adalah melakukan Exploratory Data Analysis (EDA) untuk memahami pola, distribusi, dan hubungan yang terdapat di dalam data.

📚 Referensi
Python Documentation — dokumentasi resmi bahasa pemrograman Python.
Pandas Documentation — dokumentasi resmi library Pandas.
Google Colab — platform notebook berbasis cloud untuk menjalankan kode Python.
✍️ Penulis

Maulana Aldi Pradana

Lihat portofolio penulis → [Link portofolio industri]

🏷️ Tags

Data Cleaning, Data Analysis, Python, Pandas, Google Colab, Data Science, Belajar Python, Dataset, Data Quality, Data Preparation, Analisis Data, Python Programming, Edusoft, Data Processing, Pemula
