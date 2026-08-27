# Standar & Strategi Blog IT — PKL TJKT

**Versi:** 1.0
**Tanggal:** 27 Agustus 2026
**Status:** Dokumen Acuan Proyek

---

## 1. Tujuan Proyek

Blog ini tidak dibuat hanya untuk memenuhi tugas PKL/sekolah, tetapi dirancang sebagai **blog edukasi IT yang dapat berkembang menjadi aset jangka panjang dan berpotensi dimonetisasi**.

Tugas sekolah digunakan sebagai titik awal untuk membangun kumpulan artikel yang:

* informatif;
* praktis;
* dapat dipraktikkan;
* mudah dipahami pemula;
* memiliki nilai pencarian di mesin pencari;
* saling terhubung;
* dapat dikembangkan menjadi knowledge base IT berbahasa Indonesia.

### Prinsip Utama

> **Artikel → menjelaskan konsep.**
> **Command/praktik → menunjukkan cara.**
> **Screenshot → membuktikan praktik.**
> **Studi kasus → menunjukkan penerapan.**
> **SEO → membuat artikel mudah ditemukan.**

---

## 2. Platform

### Platform Utama: Blogger / Blogspot

Blogger dipilih sebagai platform awal.

### Alasan

* Gratis.
* Mudah digunakan.
* Tidak membutuhkan pengelolaan hosting sendiri.
* Mendukung artikel, gambar, heading, kode, dan hyperlink.
* Cocok untuk dokumentasi belajar.
* Bisa digunakan untuk membangun traffic organik.
* Biaya awal sangat rendah sehingga fokus dapat diarahkan ke konten.

### Strategi Jangka Panjang

Tidak perlu langsung membeli hosting atau domain.

```text
Blogger
   ↓
Bangun konten
   ↓
Uji traffic & search demand
   ↓
Bangun topical authority
   ↓
Monetisasi
   ↓
Jika sudah layak → pertimbangkan custom domain / WordPress self-hosted
```

Migrasi platform hanya dilakukan jika memang memberikan manfaat yang jelas.

---

## 3. Positioning Blog

Blog tidak diposisikan hanya sebagai:

> "Blog tentang Linux."

Positioning yang digunakan:

> **Panduan IT praktis untuk belajar Linux, networking, server, dan troubleshooting dari dasar.**

Dengan positioning ini, blog dapat berkembang dari materi sekolah menjadi resource IT yang lebih luas.

---

## 4. Niche Utama

Fokus utama:

1. **Linux**
2. **Networking**
3. **Server**
4. **Troubleshooting**
5. **IT Fundamental**

Kelima topik tersebut saling berhubungan sehingga memungkinkan pembentukan **content cluster** dan internal linking.

---

## 5. Target Pembaca

### Level 1 — Pelajar

Contoh:

* siswa SMK TJKT;
* siswa bidang IT;
* pemula yang baru mengenal Linux/networking.

Kebutuhan:

* penjelasan sederhana;
* contoh command;
* praktik;
* screenshot;
* istilah teknis yang dijelaskan.

Contoh pencarian:

* `perintah dasar Linux`
* `cara menggunakan Linux`
* `cara setting IP`
* `apa itu subnetting`

---

### Level 2 — Pemula Belajar Mandiri

Karakteristik:

* sudah mengenal komputer;
* mulai belajar Linux/server;
* belum memahami administrasi sistem secara mendalam.

Kebutuhan:

* tutorial step-by-step;
* contoh nyata;
* penjelasan error;
* solusi yang dapat langsung dicoba.

Contoh pencarian:

* `cara membuat user Linux`
* `cara connect SSH`
* `permission denied Linux`
* `cara cek disk Linux`

---

### Level 3 — Mahasiswa / Junior IT

Karakteristik:

* lebih memahami istilah teknis;
* mencari solusi terhadap masalah tertentu;
* lebih berorientasi pada command dan konfigurasi.

Contoh pencarian:

* `systemctl service failed`
* `linux disk full`
* `ssh permission denied`
* `nginx 502 bad gateway`
* `chmod 755 meaning`

Kebutuhan utama:

> **Masalah → penyebab → command → solusi.**

---

### Level 4 — Junior SysAdmin / IT Support

Topik yang relevan:

* troubleshooting;
* server;
* networking;
* monitoring;
* log;
* service;
* deployment;
* konfigurasi.

Contoh artikel:

> **10 Cara Mengecek Penyebab Server Linux Lambat**

Target ini memiliki nilai jangka panjang karena kebutuhan informasinya lebih praktis dan spesifik.

---

## 6. Gaya Bahasa

Bahasa utama:

> **Bahasa Indonesia dengan terminologi teknis Inggris yang memang lazim digunakan di bidang IT.**

### Karakter Bahasa

* teknis;
* jelas;
* natural;
* beginner-friendly;
* tidak terlalu akademis;
* tidak terlalu slang;
* tidak menggunakan gaya "AI banget";
* tetap akurat secara teknis.

### Istilah yang Dipertahankan

Gunakan istilah yang memang digunakan praktisi:

* server
* client
* command
* terminal
* filesystem
* permission
* process
* service
* network
* IP address
* troubleshooting
* deployment
* monitoring

Hindari menerjemahkan istilah teknis secara paksa jika istilah Inggrisnya lebih umum digunakan.

---

## 7. Rasio Bahasa

Target gaya bahasa:

* **70% mudah dipahami pemula**
* **30% terminologi teknis**

Contoh:

> `systemctl` adalah command yang digunakan untuk berinteraksi dengan systemd, sistem init dan service manager yang digunakan pada banyak distribusi Linux modern.

Pemula tetap dapat memahami fungsi dasarnya, sementara terminologi teknis tetap dipertahankan.

---

## 8. Struktur Umum Artikel

Template dasar:

```text
JUDUL

Pendahuluan

Daftar Isi

1. Mengenal [Topik]
   Penjelasan konsep

2. Persiapan
   Tools/environment

3. [Materi Utama #1]
   Penjelasan
   Syntax
   Contoh
   Screenshot
   Penjelasan output

4. [Materi Utama #2]
   Penjelasan
   Syntax
   Contoh
   Screenshot
   Penjelasan output

5. [Materi Utama #3]
   ...

6. Studi Kasus / Praktik
   Skenario
   Langkah praktik
   Hasil
   Screenshot

7. Kesalahan Umum
   Error
   Penyebab
   Solusi

8. Kesimpulan

FAQ jika relevan

Referensi
```

Tidak semua bagian wajib digunakan pada artikel pendek. Struktur disesuaikan dengan search intent dan kedalaman materi.

---

## 9. Struktur Setiap Materi / Command

Setiap command atau konsep penting menggunakan pola:

```text
Nama Perintah

Fungsi

Syntax

Contoh

Penjelasan

Output

Kapan digunakan?
```

Tujuannya agar pembaca tidak hanya menghafal command, tetapi memahami fungsi dan konteks penggunaannya.

---

## 10. Screenshot / Bukti Praktik

Screenshot dianggap sebagai **bukti praktik**, bukan sekadar dekorasi artikel.

### Jumlah

**Minimum:**

> 5 screenshot per artikel

**Target ideal:**

> 8–12 screenshot per artikel

**Artikel tutorial besar:**

> 10–15 screenshot atau sesuai kebutuhan materi.

Tidak perlu membuat screenshot untuk setiap command.

Screenshot diprioritaskan pada:

* environment;
* praktik command utama;
* konfigurasi;
* hasil perubahan;
* monitoring;
* troubleshooting;
* studi kasus.

---

## 11. Standar Screenshot

Screenshot harus:

* menunjukkan command yang dijalankan;
* menunjukkan output jika relevan;
* cukup besar untuk dibaca;
* tidak terpotong pada bagian penting;
* menggunakan terminal yang jelas;
* tidak menampilkan password/token/API key;
* tidak menampilkan data pribadi;
* memiliki konteks yang jelas.

### Caption

Setiap screenshot penting diberi caption.

Format:

> **Gambar X. [Deskripsi aktivitas yang dilakukan].**

Contoh:

> **Gambar 3. Praktik penggunaan `df -h` untuk melihat penggunaan storage Linux.**

---

## 12. Panjang Artikel

Tidak ada target jumlah kata yang dipaksakan.

Kualitas dan search intent lebih penting daripada word count.

| Jenis          |           Target |
| -------------- | ---------------: |
| Artikel kecil  |   800–1.200 kata |
| Artikel normal | 1.500–2.500 kata |
| Tutorial utama | 2.500–4.000 kata |
| Tutorial besar |      4.000+ kata |

Untuk artikel besar seperti **Perintah Dasar Linux**, target awal dapat berada di kisaran **3.000–4.500 kata**, selama seluruh materi memang relevan.

> Lebih baik artikel 3.000 kata yang berguna daripada 5.000 kata yang penuh pengulangan.

---

## 13. SEO Strategy

SEO tidak dilakukan dengan keyword stuffing.

Fokus utama:

> **Search intent + kualitas jawaban + struktur + topical coverage + internal linking.**

Setiap artikel minimal memiliki:

* SEO title;
* permalink yang singkat;
* meta description;
* keyword utama;
* keyword turunan;
* heading H2/H3;
* internal link;
* external reference yang relevan;
* alt text gambar;
* caption gambar;
* struktur yang mudah dipindai;
* FAQ jika memang relevan.

---

## 14. Keyword Strategy

Setiap artikel memiliki:

### Keyword Utama

Contoh:

> `perintah dasar Linux`

### Keyword Turunan

Contoh:

* perintah Linux;
* command Linux;
* Linux untuk pemula;
* perintah dasar Linux untuk server;
* command terminal Linux;
* administrasi server Linux.

Keyword digunakan secara natural dan tidak dipaksakan.

---

## 15. Search Intent

Sebelum menulis artikel, tentukan tujuan pencarian pembaca.

### Informational

Pembaca ingin memahami sesuatu.

Contoh:

> `apa itu Linux`

### Tutorial / How-to

Pembaca ingin melakukan sesuatu.

Contoh:

> `cara install nginx Ubuntu`

### Troubleshooting

Pembaca mengalami masalah.

Contoh:

> `permission denied Linux`

### Comparison

Pembaca ingin membandingkan.

Contoh:

> `Ubuntu vs Debian server`

### Reference

Pembaca membutuhkan referensi cepat.

Contoh:

> `chmod 755 meaning`

Artikel harus disusun berdasarkan intent utama, bukan sekadar berdasarkan keyword.

---

## 16. Content Cluster

Blog menggunakan struktur topical cluster.

### Pilar Linux

```text
Linux
├── Perintah Dasar Linux
├── File & Directory
├── User & Group
├── Permission
├── Process
├── Service
├── Package Management
└── Troubleshooting Linux
```

### Pilar Networking

```text
Networking
├── IP Address
├── Subnetting
├── DHCP
├── DNS
├── Routing
├── VLAN
├── NAT
└── Network Troubleshooting
```

### Pilar Server

```text
Server
├── SSH
├── Nginx
├── Apache
├── Web Server
├── Database
├── Monitoring
└── Backup
```

### Pilar Troubleshooting

```text
Troubleshooting
├── Linux tidak bisa boot
├── SSH gagal
├── Permission denied
├── Disk penuh
├── RAM penuh
├── Service gagal
├── DNS error
└── Network tidak terhubung
```

---

## 17. Internal Linking

Artikel tidak berdiri sendiri.

Contoh hubungan:

```text
Perintah Dasar Linux
        ↓
Linux File Permission
        ↓
User & Group Linux
        ↓
Process & Service Linux
        ↓
SSH Linux
        ↓
Linux Networking
        ↓
Linux Server
        ↓
Troubleshooting Server
```

Jika artikel terkait sudah tersedia, gunakan internal link secara natural.

Tujuan:

* membantu pembaca menemukan materi lanjutan;
* membangun struktur situs;
* memperkuat topical coverage;
* meningkatkan navigasi.

---

## 18. Jenis Artikel yang Diprioritaskan

Jangan hanya membuat artikel definisi.

Prioritas:

### 1. Tutorial

Cara melakukan sesuatu.

### 2. Troubleshooting

Cara menyelesaikan masalah.

### 3. Practical Guide

Panduan melakukan pekerjaan tertentu.

### 4. Reference

Command atau konfigurasi yang sering dicari.

### 5. Fundamental

Konsep dasar yang menjadi fondasi artikel lain.

Komposisi dapat disesuaikan berdasarkan data traffic dan search demand.

---

## 19. Strategi Monetisasi

Monetisasi dilakukan bertahap.

### Tahap 1 — Traffic

Fokus:

* kualitas konten;
* SEO;
* search intent;
* internal linking;
* topical authority.

Belum perlu mengejar revenue secara agresif.

### Tahap 2 — Display Ads

Model sederhana:

```text
Traffic
   ↓
Pageview
   ↓
Advertisement
   ↓
Revenue
```

Cocok ketika traffic sudah mulai signifikan.

### Tahap 3 — Affiliate

Artikel yang relevan dapat mengarah ke produk/service yang memang berguna bagi pembaca.

Prinsip:

> Jangan merekomendasikan sesuatu hanya karena komisinya.

Rekomendasi harus tetap relevan dan transparan.

### Tahap 4 — Digital Product

Potensi produk:

* Linux Cheat Sheet;
* Panduan Networking;
* Lab Linux untuk TJKT;
* Modul troubleshooting;
* Template dokumentasi server;
* materi belajar IT.

### Tahap 5 — Jasa

Dalam jangka panjang, reputasi blog dapat mendukung:

* konsultasi;
* setup server;
* maintenance;
* website;
* automation;
* layanan IT lainnya.

Tahap ini bukan target awal dan harus mengikuti kemampuan serta pengalaman nyata.

---

## 20. Prinsip Monetisasi

Blog tidak boleh berubah menjadi situs yang hanya mengejar uang.

Urutan prioritas:

```text
Kegunaan
   ↓
Kualitas
   ↓
Kepercayaan
   ↓
Traffic
   ↓
Monetisasi
```

Bukan:

```text
Monetisasi
   ↓
Keyword stuffing
   ↓
Artikel generik
   ↓
Traffic buruk
```

---

## 21. Identitas Blog

### Tema

> **Linux + Networking + Server + Troubleshooting + IT Fundamental**

### Target Pembaca

> **Pelajar → pemula → mahasiswa → junior IT**

### Karakter

> **Praktis + teknis + beginner-friendly**

### Tujuan Jangka Panjang

> **Menjadi knowledge base IT berbahasa Indonesia.**

---

## 22. Tugas Sekolah sebagai Konten Awal

Tugas PKL tidak dianggap sebagai konten terpisah dari blog.

Contoh roadmap:

```text
Tugas:
Perintah Dasar Linux
        ↓
Linux File Permission
        ↓
User & Group Linux
        ↓
Process & Service Linux
        ↓
SSH Linux
        ↓
Linux Networking
        ↓
Linux Server
        ↓
Server Troubleshooting
```

Dengan pendekatan ini:

> **Tugas sekolah menjadi fondasi content library.**

---

## 23. Standar Artikel PKL

| Komponen           | Standar                                                    |
| ------------------ | ---------------------------------------------------------- |
| Platform           | Blogger / Blogspot                                         |
| Bahasa             | Indonesia + istilah teknis Inggris                         |
| Target             | Pelajar → pemula → mahasiswa → junior IT                   |
| Niche              | Linux, Networking, Server, Troubleshooting, IT Fundamental |
| Gaya               | Teknis, jelas, natural, beginner-friendly                  |
| Daftar isi         | Untuk artikel panjang                                      |
| Screenshot         | Minimum 5                                                  |
| Screenshot ideal   | 8–12                                                       |
| Caption            | Wajib untuk screenshot penting                             |
| Contoh command     | Wajib untuk tutorial                                       |
| Praktik nyata      | Wajib jika memungkinkan                                    |
| Studi kasus        | Disarankan                                                 |
| Error/solusi       | Disarankan                                                 |
| FAQ                | Jika relevan                                               |
| Keyword utama      | 1 keyword utama                                            |
| Keyword turunan    | Beberapa keyword relevan                                   |
| SEO title          | Wajib                                                      |
| Meta description   | Wajib                                                      |
| Permalink          | Singkat dan relevan                                        |
| Heading            | H2/H3 terstruktur                                          |
| Alt text           | Wajib                                                      |
| Internal link      | Jika artikel terkait tersedia                              |
| External reference | Sumber terpercaya                                          |
| Panjang            | Menyesuaikan search intent dan materi                      |

---

## 24. Checklist Sebelum Publish

* [ ] Search intent sudah jelas
* [ ] Keyword utama sudah ditentukan
* [ ] Judul sudah dibuat
* [ ] Struktur H2/H3 sudah jelas
* [ ] Pendahuluan menjelaskan manfaat artikel
* [ ] Contoh praktik sudah tersedia
* [ ] Command sudah diuji
* [ ] Screenshot praktik sudah tersedia
* [ ] Screenshot tidak mengandung data sensitif
* [ ] Screenshot penting memiliki caption
* [ ] Internal link ditambahkan jika relevan
* [ ] External reference ditambahkan jika diperlukan
* [ ] SEO title sudah dibuat
* [ ] Meta description sudah dibuat
* [ ] Permalink sudah diperiksa
* [ ] Alt text gambar sudah diisi
* [ ] Artikel sudah diperiksa secara teknis
* [ ] Artikel sudah diperiksa typo/grammar
* [ ] Artikel dapat dipahami pembaca pemula
* [ ] Tidak ada keyword stuffing
* [ ] Artikel memberikan jawaban yang benar-benar berguna

---

## 25. Prinsip Editorial

Sebelum artikel dibuat, jawab pertanyaan berikut:

1. Apa yang ingin dicari pembaca?
2. Siapa pembacanya?
3. Apa masalah yang ingin diselesaikan?
4. Apakah contoh command benar-benar dapat digunakan?
5. Apakah pembaca pemula dapat mengikutinya?
6. Apakah artikel memberikan praktik nyata?
7. Apakah screenshot membuktikan praktik?
8. Artikel ini terhubung dengan artikel apa?
9. Apa keyword/search intent utamanya?
10. Apakah artikel tetap berguna tanpa monetisasi?

Jika jawabannya jelas, artikel dapat masuk tahap penulisan.

---

## 26. Roadmap Pengembangan

```text
FASE 1
Setup Blogger
        ↓
Identitas blog
        ↓
Template artikel
        ↓
Artikel pertama

FASE 2
Linux fundamentals
        ↓
Networking fundamentals
        ↓
Server fundamentals

FASE 3
Troubleshooting
        ↓
Practical guides
        ↓
Search-driven content

FASE 4
Internal linking
        ↓
Topical authority
        ↓
SEO refinement

FASE 5
Traffic growth
        ↓
Ads / Affiliate
        ↓
Digital product

FASE 6
Evaluasi
        ↓
Custom domain / WordPress
        ↓
Pengembangan brand
```

---

## 27. Artikel Pertama

Artikel pertama yang direncanakan:

> **Perintah Dasar Linux: Panduan Administrasi Server untuk Pemula**

Artikel ini akan menjadi **master template** untuk artikel berikutnya.

Materi utama yang direncanakan:

* informasi sistem;
* navigasi filesystem;
* manajemen file;
* membaca file;
* permission;
* user dan group;
* process;
* service;
* monitoring;
* networking;
* storage;
* package management;
* archive/compression;
* redirection dan pipe;
* bantuan Linux;
* praktik administrasi server.

---

## 28. Prinsip Akhir

Blog ini dibangun dengan mindset:

> **"Saya sedang membangun dokumentasi IT yang dimulai dari tugas sekolah."**

Bukan:

> **"Saya sedang membuat kumpulan artikel untuk menyelesaikan tugas."**

Setiap artikel harus memiliki nilai yang tetap berguna bagi pembaca meskipun tugas sekolah sudah selesai.

### Target Akhir

> Sebuah knowledge base IT berbahasa Indonesia yang dimulai dari Linux dan berkembang ke networking, server, serta troubleshooting, dengan fondasi SEO dan monetisasi yang sehat.
