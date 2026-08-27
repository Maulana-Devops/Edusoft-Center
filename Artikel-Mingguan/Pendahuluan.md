Siap. Berikut versi **`README.md`** yang sudah diperbarui untuk keputusan **Medium + GitHub**, dan bisa langsung kamu copy ke repository GitHub.

````markdown
# Strategi Blog IT — PKL TJKT

> Dokumen acuan utama untuk membangun blog/artikel IT sebagai bagian dari PKL TJKT sekaligus membangun portofolio dan aset konten jangka panjang.

**Versi:** 2.0  
**Tanggal:** 27 Agustus 2026  
**Platform Publikasi:** Medium  
**Repository:** GitHub  
**Bahasa:** Bahasa Indonesia

---

## 1. Tujuan Proyek

Proyek ini tidak dibuat hanya untuk memenuhi tugas sekolah.

Tugas PKL digunakan sebagai titik awal untuk membangun **knowledge base IT berbahasa Indonesia** yang dapat berkembang menjadi:

- portofolio IT;
- dokumentasi pembelajaran;
- sumber referensi bagi pemula;
- media untuk membangun reputasi;
- aset konten jangka panjang;
- media yang berpotensi dimonetisasi.

Prinsip utama:

> **Tugas sekolah → artikel → knowledge base → portofolio → readership → monetisasi**

---

# 2. Platform

## Platform Publikasi: Medium

Artikel akan dipublikasikan menggunakan **Medium**.

### Alasan memilih Medium

- Tidak perlu mengelola hosting.
- Tidak perlu membuat template website dari awal.
- Fokus dapat diarahkan pada kualitas tulisan.
- Tampilan artikel sudah cukup profesional.
- Mendukung gambar, heading, code block, quote, list, dan link.
- Cocok untuk membangun portofolio tulisan.
- Artikel dapat dibagikan dengan mudah.
- Memiliki ekosistem pembaca sendiri.

### GitHub sebagai Source of Truth

Medium digunakan sebagai **tempat publikasi**.

GitHub digunakan sebagai **tempat menyimpan source artikel**.

```text
GitHub
   │
   ├── Markdown
   ├── Gambar
   ├── Draft
   └── Dokumentasi
          ↓
       Medium
          ↓
      Published
          ↓
   Portfolio / Readers
````

Keuntungan:

* artikel memiliki backup;
* mudah diedit;
* mudah digunakan bersama AI;
* mudah dipindahkan ke platform lain;
* histori perubahan dapat disimpan;
* struktur konten lebih terorganisir.

---

# 3. Positioning

Blog tidak diposisikan hanya sebagai:

> "Blog tentang Linux."

Positioning utama:

> **Panduan IT praktis untuk belajar Linux, networking, server, dan troubleshooting dari dasar.**

Target jangka panjang:

> **Knowledge base IT berbahasa Indonesia yang praktis dan mudah dipahami.**

---

# 4. Niche

Fokus utama:

1. Linux
2. Networking
3. Server
4. Troubleshooting
5. IT Fundamental

Kelima topik tersebut saling berhubungan dan dapat membentuk **content cluster**.

```text
IT Fundamental
      │
      ├── Linux
      │
      ├── Networking
      │
      ├── Server
      │
      └── Troubleshooting
```

---

# 5. Target Pembaca

## Level 1 — Pelajar

Target utama:

* siswa SMK TJKT;
* siswa bidang IT;
* pemula yang baru belajar Linux;
* pelajar yang ingin memahami networking dan server.

Kebutuhan:

* bahasa sederhana;
* contoh nyata;
* command;
* screenshot;
* langkah praktik.

---

## Level 2 — Pemula Belajar Mandiri

Karakteristik:

* sudah mengenal komputer;
* mulai belajar Linux/server;
* belum memahami administrasi sistem secara mendalam.

Kebutuhan:

* tutorial step-by-step;
* contoh;
* troubleshooting;
* penjelasan error.

---

## Level 3 — Mahasiswa / Junior IT

Karakteristik:

* sudah mengenal istilah teknis;
* mencari solusi praktis;
* membutuhkan referensi command dan konfigurasi.

Contoh pencarian:

```text
systemctl service failed
linux disk full
ssh permission denied
nginx 502 bad gateway
chmod 755 meaning
```

Format yang disukai:

> **Masalah → Penyebab → Solusi → Command → Hasil**

---

## Level 4 — Junior SysAdmin / IT Support

Topik:

* server;
* networking;
* monitoring;
* log;
* service;
* deployment;
* troubleshooting.

Target ini merupakan target jangka panjang.

---

# 6. Bahasa

## Bahasa Utama

> **Bahasa Indonesia**

Bahasa Indonesia digunakan karena target utama adalah pembaca Indonesia.

Namun, terminologi teknis tetap menggunakan istilah yang umum digunakan di industri IT.

### Contoh istilah

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

Jangan menerjemahkan istilah teknis secara paksa jika istilah Inggris lebih umum digunakan.

---

# 7. Gaya Bahasa

Karakter tulisan:

* teknis;
* jelas;
* natural;
* praktis;
* beginner-friendly;
* tidak terlalu akademis;
* tidak terlalu slang;
* tidak bertele-tele;
* akurat secara teknis.

Target:

> **70% mudah dipahami pemula + 30% terminologi teknis**

Contoh:

> `systemctl` adalah command yang digunakan untuk berinteraksi dengan systemd, yaitu sistem init dan service manager yang digunakan pada banyak distribusi Linux modern.

---

# 8. Prinsip Penulisan

Artikel harus menjawab:

1. Apa yang ingin dicari pembaca?
2. Siapa pembacanya?
3. Apa masalah yang ingin diselesaikan?
4. Apa konsep yang perlu dipahami?
5. Bagaimana cara mempraktikkannya?
6. Apa hasil yang seharusnya muncul?
7. Apa kesalahan yang mungkin terjadi?
8. Apa solusi jika terjadi error?

Prinsip utama:

> **Jangan hanya menjelaskan apa. Jelaskan juga bagaimana dan kapan digunakan.**

---

# 9. Struktur Artikel

Template dasar:

````text
TITLE

SUBTITLE / DESCRIPTION

INTRODUCTION

TABLE OF CONTENTS
(optional untuk artikel panjang)

## 1. Mengenal [Topik]

Penjelasan konsep.

## 2. Persiapan

Tools / environment yang dibutuhkan.

## 3. [Materi Utama]

Penjelasan.

### Fungsi

### Syntax

```bash
command
````

### Contoh

```bash
command
```

### Output

Screenshot / output terminal.

Penjelasan hasil.

## 4. Praktik

Skenario nyata.

Langkah:

1. ...
2. ...
3. ...

Screenshot praktik.

## 5. Kesalahan Umum

### Error 1

Penyebab.

Solusi.

### Error 2

Penyebab.

Solusi.

## 6. Kesimpulan

Ringkasan.

## 7. Referensi

Sumber resmi / terpercaya.

````

---

# 10. Struktur Setiap Command

Setiap command penting menggunakan pola:

```text
Nama Command

Fungsi

Syntax

Contoh

Output

Penjelasan Output

Kapan digunakan?

Catatan
````

Contoh:

```bash
df -h
```

Penjelasan harus mencakup:

* apa fungsi `df`;
* apa fungsi option `-h`;
* contoh penggunaan;
* bagaimana membaca output;
* kapan command berguna.

---

# 11. Screenshot

Screenshot berfungsi sebagai **bukti praktik**.

Screenshot bukan sekadar dekorasi.

## Jumlah

### Minimum

> **5 screenshot per artikel**

### Ideal

> **8–12 screenshot per artikel**

### Tutorial besar

> **10–15 screenshot**, disesuaikan dengan kebutuhan.

Tidak semua command harus memiliki screenshot.

Prioritaskan:

* environment;
* command utama;
* konfigurasi;
* hasil perubahan;
* monitoring;
* troubleshooting;
* studi kasus.

---

# 12. Standar Screenshot

Screenshot harus:

* jelas;
* cukup besar;
* command dapat dibaca;
* output dapat dibaca;
* tidak terpotong;
* memiliki konteks;
* menunjukkan praktik nyata.

Jangan menampilkan:

* password;
* API key;
* token;
* private key;
* data pribadi;
* informasi sensitif.

---

# 13. Caption Screenshot

Screenshot penting diberikan caption.

Format:

> **Gambar X. [Deskripsi aktivitas].**

Contoh:

> **Gambar 3. Hasil penggunaan `df -h` untuk melihat penggunaan storage Linux.**

Caption harus menjelaskan **apa yang sedang ditunjukkan**, bukan hanya "Screenshot terminal".

---

# 14. SEO

SEO tetap diperhatikan, tetapi bukan satu-satunya sumber traffic.

Strategi:

```text
Search Intent
     ↓
Keyword
     ↓
Content Quality
     ↓
Structure
     ↓
Internal / External Links
     ↓
Search Visibility
```

Karena platform menggunakan Medium, fokus SEO tidak hanya pada Google tetapi juga pada **keterbacaan dan relevansi bagi pembaca Medium**.

---

# 15. Keyword Strategy

Setiap artikel memiliki:

### Primary Keyword

Satu keyword utama.

Contoh:

```text
perintah dasar Linux
```

### Secondary Keywords

Contoh:

```text
perintah Linux
command Linux
Linux untuk pemula
command terminal Linux
perintah Linux untuk server
administrasi server Linux
```

Keyword harus digunakan secara natural.

Hindari:

> keyword stuffing

---

# 16. Search Intent

Sebelum menulis artikel, tentukan search intent.

## Informational

Pembaca ingin memahami konsep.

Contoh:

```text
apa itu Linux
apa itu SSH
apa itu DNS
```

## Tutorial / How-to

Pembaca ingin melakukan sesuatu.

Contoh:

```text
cara install nginx Ubuntu
cara membuat user Linux
cara konfigurasi SSH
```

## Troubleshooting

Pembaca mengalami masalah.

Contoh:

```text
permission denied Linux
SSH connection refused
disk full Linux
nginx 502
```

## Reference

Pembaca membutuhkan referensi cepat.

Contoh:

```text
chmod 755 meaning
Linux commands list
systemctl commands
```

Artikel harus mengikuti intent utama.

---

# 17. Content Cluster

## Linux

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

## Networking

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

## Server

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

## Troubleshooting

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

# 18. Internal Linking

Artikel harus saling terhubung jika memiliki hubungan topik.

Contoh:

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

Tujuan:

* membantu pembaca menemukan artikel terkait;
* membangun struktur knowledge base;
* meningkatkan navigasi;
* memperkuat topical coverage.

---

# 19. Jenis Artikel Prioritas

Prioritas konten:

### 1. Tutorial

Cara melakukan sesuatu.

### 2. Troubleshooting

Cara menyelesaikan masalah.

### 3. Practical Guide

Panduan melakukan pekerjaan tertentu.

### 4. Reference

Referensi command/configuration.

### 5. Fundamental

Konsep dasar.

Artikel definisi tetap dibuat jika diperlukan, tetapi tidak menjadi satu-satunya jenis konten.

---

# 20. Strategi Traffic

Karena menggunakan Medium, traffic berasal dari beberapa sumber.

```text
                ┌── Google Search
                │
Medium ─────────┼── Medium Readers
                │
                ├── Publication
                │
                └── Social / Community
```

Prioritas:

1. kualitas artikel;
2. search intent;
3. judul yang jelas;
4. readability;
5. konsistensi;
6. distribusi artikel;
7. internal linking.

---

# 21. Monetisasi

Monetisasi dilakukan bertahap.

## Tahap 1 — Build

Fokus:

* artikel;
* kualitas;
* consistency;
* readership;
* portfolio.

## Tahap 2 — Audience

Fokus:

* meningkatkan pembaca;
* mengidentifikasi artikel populer;
* memahami topik yang memiliki demand.

## Tahap 3 — Monetization

Potensi:

* program monetisasi platform jika memenuhi syarat;
* affiliate;
* digital product;
* jasa;
* sponsorship yang relevan.

Monetisasi harus mengikuti aturan platform yang berlaku.

---

# 22. Prinsip Monetisasi

Urutan prioritas:

```text
Kegunaan
   ↓
Kualitas
   ↓
Kepercayaan
   ↓
Pembaca
   ↓
Reputasi
   ↓
Monetisasi
```

Bukan:

```text
Monetisasi
   ↓
Clickbait
   ↓
Artikel generik
   ↓
Keyword stuffing
   ↓
Pembaca tidak percaya
```

---

# 23. GitHub Repository Structure

Struktur repository yang disarankan:

```text
blog-it/
│
├── README.md
│
├── articles/
│   ├── linux/
│   │   ├── perintah-dasar-linux.md
│   │   ├── linux-file-permission.md
│   │   └── user-group-linux.md
│   │
│   ├── networking/
│   │   ├── ip-address.md
│   │   └── subnetting.md
│   │
│   ├── server/
│   │   ├── ssh.md
│   │   └── nginx.md
│   │
│   └── troubleshooting/
│
├── assets/
│   ├── images/
│   └── screenshots/
│
├── drafts/
│
└── research/
```

---

# 24. Workflow Artikel

Setiap artikel mengikuti workflow:

```text
01. Tentukan topik
        ↓
02. Tentukan target pembaca
        ↓
03. Riset search intent
        ↓
04. Tentukan keyword
        ↓
05. Buat judul
        ↓
06. Buat outline
        ↓
07. Riset materi
        ↓
08. Praktikkan command
        ↓
09. Ambil screenshot
        ↓
10. Tulis artikel Markdown
        ↓
11. Review teknis
        ↓
12. Review bahasa
        ↓
13. Optimasi SEO
        ↓
14. Publish ke Medium
        ↓
15. Simpan versi final di GitHub
        ↓
16. Pantau performa
```

---

# 25. Checklist Sebelum Publish

## Content

* [ ] Search intent sudah jelas
* [ ] Target pembaca sudah jelas
* [ ] Keyword utama sudah ditentukan
* [ ] Judul sudah jelas
* [ ] Artikel memberikan solusi nyata
* [ ] Konsep teknis benar
* [ ] Command sudah diuji
* [ ] Output sudah diverifikasi
* [ ] Tidak ada informasi yang mengada-ada

## Screenshot

* [ ] Minimal 5 screenshot
* [ ] Screenshot dapat dibaca
* [ ] Command terlihat
* [ ] Output terlihat jika diperlukan
* [ ] Screenshot memiliki konteks
* [ ] Screenshot penting memiliki caption
* [ ] Tidak ada password/token/API key
* [ ] Tidak ada data pribadi

## SEO

* [ ] Primary keyword
* [ ] Secondary keywords
* [ ] Judul relevan
* [ ] Heading terstruktur
* [ ] Keyword digunakan secara natural
* [ ] Internal link jika tersedia
* [ ] External reference jika diperlukan
* [ ] Tidak ada keyword stuffing

## Medium

* [ ] Judul sudah diperiksa
* [ ] Subtitle/description sudah jelas
* [ ] Heading sudah benar
* [ ] Code block sudah benar
* [ ] Gambar tidak rusak
* [ ] Link berfungsi
* [ ] Preview sudah diperiksa
* [ ] Tampilan mobile diperiksa
* [ ] Artikel sudah dipublish

## GitHub

* [ ] Markdown final disimpan
* [ ] Screenshot/assets tersimpan
* [ ] Nama file konsisten
* [ ] Struktur folder benar
* [ ] Commit message jelas

---

# 26. Editorial Checklist

Sebelum artikel dianggap selesai, tanyakan:

1. Apakah artikel benar-benar menjawab pertanyaan pembaca?
2. Apakah pembaca pemula dapat mengikutinya?
3. Apakah command sudah diuji?
4. Apakah screenshot merupakan bukti praktik nyata?
5. Apakah penjelasan teknis benar?
6. Apakah ada bagian yang hanya mengulang informasi?
7. Apakah artikel mempunyai search intent yang jelas?
8. Apakah artikel terhubung dengan artikel lain?
9. Apakah judul sesuai dengan isi?
10. Apakah artikel tetap berguna tanpa monetisasi?

---

# 27. Artikel Pertama

## Judul

> **Perintah Dasar Linux: Panduan Administrasi Server untuk Pemula**

Artikel pertama akan menjadi **master template** untuk artikel berikutnya.

### Materi yang direncanakan

* informasi sistem;
* navigasi filesystem;
* manajemen file;
* membaca file;
* user dan group;
* permission;
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

# 28. Roadmap Konten

```text
PERINTAH DASAR LINUX
        ↓
FILE & DIRECTORY
        ↓
USER & GROUP
        ↓
FILE PERMISSION
        ↓
PROCESS
        ↓
SERVICE
        ↓
SYSTEM MONITORING
        ↓
LINUX NETWORKING
        ↓
SSH
        ↓
WEB SERVER
        ↓
SERVER ADMINISTRATION
        ↓
TROUBLESHOOTING
```

Kemudian berkembang ke:

```text
Linux
 ├── Networking
 ├── Server
 ├── Security
 ├── Cloud
 ├── DevOps
 └── Automation
```

Pengembangan dilakukan berdasarkan kemampuan, pengalaman, dan demand pembaca.

---

# 29. Prinsip Akhir

Blog ini dibangun dengan mindset:

> **"Saya sedang membangun dokumentasi IT yang dimulai dari tugas sekolah."**

Bukan:

> **"Saya sedang membuat kumpulan artikel untuk menyelesaikan tugas."**

Setiap artikel harus mempunyai nilai yang tetap berguna bagi pembaca setelah tugas sekolah selesai.

### Target Akhir

> **Membangun knowledge base IT berbahasa Indonesia yang praktis, akurat, beginner-friendly, memiliki nilai portofolio, dan memiliki peluang untuk berkembang menjadi aset yang dapat dimonetisasi.**

---

## Status Proyek

**Platform:** Medium
**Repository:** GitHub
**Bahasa:** Indonesia
**Niche:** Linux / Networking / Server / Troubleshooting
**Target:** Pelajar → Pemula → Mahasiswa → Junior IT
**Artikel pertama:** Perintah Dasar Linux
**Status:** Perencanaan

```
```
