# Mengenal DNS: Bagaimana Domain Menemukan Alamat Server?

Saat membuka sebuah website, kita biasanya cukup mengetikkan nama domain seperti `google.com` ke browser. Dalam beberapa saat, halaman website akan muncul. Namun, komputer sebenarnya berkomunikasi menggunakan alamat IP, bukan nama domain yang mudah diingat manusia.

Di sinilah DNS berperan. DNS membantu menerjemahkan nama domain menjadi informasi yang dibutuhkan komputer untuk menemukan server tujuan. Tanpa DNS, pengguna harus mengingat alamat IP setiap website yang ingin dikunjungi.

Pada artikel ini, kita akan mengenal pengertian DNS, memahami proses kerjanya, mempelajari beberapa jenis DNS record, serta melakukan praktik DNS lookup menggunakan Windows PowerShell.

## 1. Apa Itu DNS?

DNS merupakan singkatan dari Domain Name System, yaitu sistem yang digunakan untuk mencari informasi berdasarkan nama domain. Salah satu fungsi yang paling dikenal adalah menerjemahkan nama domain menjadi alamat IP.

Sebagai contoh, ketika kita membuka `google.com`, browser membutuhkan alamat IP untuk menghubungi server tujuan. DNS membantu menemukan informasi alamat tersebut sehingga pengguna tidak perlu menghafalnya secara manual.

Secara sederhana, DNS dapat dianalogikan seperti buku kontak pada ponsel. Kita cukup mencari nama seseorang untuk menemukan nomor teleponnya. Dengan cara serupa, komputer menggunakan DNS untuk mencari informasi yang berkaitan dengan sebuah domain.

Namun, DNS tidak hanya menyimpan alamat IP. Sistem ini juga menyediakan informasi lain, seperti server email, nameserver, dan data verifikasi domain.

## 2. Perbedaan Domain dan IP Address

Sebelum memahami proses DNS, kita perlu mengetahui perbedaan antara domain dan IP address.

Domain adalah nama yang digunakan untuk mengakses suatu layanan di internet. Contohnya adalah `google.com` dan `cloudflare.com`. Nama tersebut lebih mudah diingat dibandingkan deretan angka atau karakter alamat jaringan.

Sementara itu, IP address merupakan alamat numerik yang digunakan untuk mengidentifikasi perangkat atau layanan dalam jaringan IP.

Ada dua versi alamat IP yang umum digunakan:

- IPv4: menggunakan alamat 32-bit, contohnya `172.217.194.100`.
- IPv6: menggunakan alamat 128-bit, contohnya `2404:6800:4003:c04::66`.

Dengan demikian, domain dan IP address memiliki fungsi yang berbeda, tetapi saling berkaitan. Domain memudahkan manusia mengenali layanan, sedangkan IP address digunakan dalam komunikasi jaringan.

## 3. Bagaimana Cara Kerja DNS?

Ketika pengguna mengetikkan nama domain di browser, sistem akan mencari informasi DNS agar dapat menemukan alamat tujuan.

Secara umum, proses DNS resolution berlangsung melalui beberapa tahapan berikut:

1. Pengguna memasukkan nama domain, misalnya `google.com`, ke browser.
2. Sistem memeriksa informasi DNS yang mungkin sudah tersimpan di cache lokal.
3. Jika informasi belum tersedia, permintaan diteruskan ke DNS resolver yang digunakan perangkat.
4. Resolver memeriksa cache miliknya. Apabila masih belum menemukan jawaban, resolver dapat mencari informasi melalui hierarki DNS.
5. Resolver menghubungi root DNS server untuk memperoleh petunjuk menuju nameserver domain tingkat atas atau TLD.
6. Selanjutnya, resolver memperoleh petunjuk menuju authoritative DNS server yang mengelola informasi domain tersebut.
7. Authoritative DNS server memberikan record DNS yang diminta.
8. Resolver mengirimkan hasilnya kembali kepada perangkat, kemudian browser dapat melanjutkan koneksi ke server tujuan.

Perlu diketahui bahwa proses tersebut merupakan gambaran umum. Dalam praktiknya, beberapa tahapan dapat dilewati karena informasi sudah tersedia di cache resolver atau perangkat.

[Tempatkan ilustrasi alur DNS resolution di sini jika tersedia.]

## 4. Mengenal Jenis-Jenis DNS Record

DNS menggunakan berbagai jenis record untuk menyimpan informasi mengenai sebuah domain. Setiap record memiliki fungsi yang berbeda.

Berikut beberapa jenis DNS record yang sering ditemukan:

### A Record

A record digunakan untuk menghubungkan nama domain dengan alamat IPv4.

Contohnya, sebuah domain dapat memiliki A record yang mengarah ke alamat `172.217.194.100`.

### AAAA Record

AAAA record memiliki fungsi serupa dengan A record, tetapi digunakan untuk menghubungkan domain dengan alamat IPv6.

Dengan adanya record ini, domain dapat menyediakan informasi alamat IPv6 bagi perangkat yang mendukungnya.

### CNAME Record

CNAME atau Canonical Name digunakan untuk membuat alias dari suatu nama domain ke nama domain lainnya.

Sebagai contoh, sebuah subdomain dapat diarahkan ke nama domain lain tanpa harus menyimpan alamat IP secara langsung pada record tersebut.

### MX Record

MX atau Mail Exchange digunakan untuk menunjukkan server yang bertugas menerima email untuk suatu domain.

Record ini memiliki nilai preference atau prioritas. Semakin kecil angka preference, semakin tinggi prioritas server tersebut.

### NS Record

NS atau Name Server menunjukkan nameserver yang berwenang mengelola informasi DNS untuk suatu domain.

Dengan kata lain, record ini membantu menunjukkan server DNS yang menjadi sumber informasi otoritatif bagi domain tersebut.

### TXT Record

TXT record digunakan untuk menyimpan informasi berbentuk teks pada DNS.

Salah satu penggunaannya adalah verifikasi kepemilikan domain dan penyimpanan kebijakan email seperti SPF. Perlu dicatat bahwa SPF bukan jenis record DNS tersendiri dalam praktik DNS modern, melainkan kebijakan yang umumnya dipublikasikan menggunakan TXT record.

## 5. Apa Itu DNS Lookup?

DNS lookup adalah proses untuk mencari informasi DNS berdasarkan nama domain atau jenis record tertentu.

Proses ini berguna ketika kita ingin mengetahui alamat IP sebuah domain, memeriksa nameserver, atau melihat informasi server email.

Selain melalui aplikasi berbasis web, DNS lookup dapat dilakukan langsung dari terminal. Pada Windows, kita dapat menggunakan dua tools bawaan, yaitu `nslookup` dan `Resolve-DnsName`.

Keduanya dapat membantu administrator jaringan maupun engineer ketika melakukan pemeriksaan awal terhadap konfigurasi DNS.

## 6. Praktik DNS Lookup Menggunakan Windows PowerShell

Pada praktik kali ini, kita akan menggunakan Windows PowerShell untuk memeriksa beberapa informasi DNS dari domain publik.

### A. Memeriksa Tools DNS

Pertama, buka Windows PowerShell. Kemudian, jalankan perintah berikut untuk memastikan tools yang diperlukan tersedia:

```powershell
Get-Command nslookup
Get-Command Resolve-DnsName
```

Perintah `Get-Command` digunakan untuk memeriksa apakah suatu perintah tersedia di lingkungan PowerShell.

Pada komputer yang digunakan dalam praktik ini, kedua tools berhasil ditemukan. `nslookup` terdeteksi sebagai aplikasi, sedangkan `Resolve-DnsName` tersedia sebagai cmdlet PowerShell.

[SCREENSHOT 01]
Nama file: 01-memeriksa-tools-dns.png
Caption: Memeriksa ketersediaan nslookup dan Resolve-DnsName melalui Windows PowerShell.
Alt text: Pemeriksaan tools nslookup dan Resolve-DnsName di Windows PowerShell.

### B. Melakukan DNS Lookup Sederhana

Setelah memastikan tools tersedia, kita dapat melakukan pencarian DNS sederhana menggunakan perintah berikut:

```powershell
nslookup google.com
```

Perintah tersebut meminta informasi DNS untuk domain `google.com`.

Hasil praktik menampilkan beberapa informasi, termasuk DNS server yang digunakan serta alamat IPv4 dan IPv6 milik domain tersebut.

Pada output, terdapat keterangan `Server: UnKnown` dengan alamat `fe80::1`. Artinya, resolver yang digunakan memiliki alamat IPv6 link-local tersebut, tetapi nama servernya tidak berhasil ditampilkan oleh `nslookup`.

Selain itu, terdapat keterangan `Non-authoritative answer`. Keterangan ini menunjukkan bahwa jawaban diberikan oleh server yang bukan authoritative DNS server untuk domain tersebut, biasanya melalui layanan recursive resolver.

[SCREENSHOT 02]
Nama file: 02-nslookup-google.png
Caption: Melakukan DNS lookup sederhana untuk domain google.com menggunakan nslookup.
Alt text: Hasil perintah nslookup google.com di Windows PowerShell.

### C. Memeriksa A dan AAAA Record

Selanjutnya, kita akan mencari alamat IPv4 dan IPv6 secara terpisah.

Untuk memeriksa A record, jalankan:

```powershell
nslookup -type=A google.com
```

Sementara itu, perintah berikut digunakan untuk memeriksa AAAA record:

```powershell
nslookup -type=AAAA google.com
```

Hasil pemeriksaan A record menampilkan beberapa alamat IPv4. Sebagai contoh, salah satu alamat yang diperoleh adalah `172.217.194.139`.

Di sisi lain, pemeriksaan AAAA record menampilkan alamat IPv6, seperti `2404:6800:4003:c04::71`.

Perbedaan hasil tersebut menunjukkan bahwa satu domain dapat memiliki beberapa alamat IP, baik IPv4 maupun IPv6. Jumlah dan alamat yang muncul juga dapat berubah bergantung pada resolver, lokasi, serta konfigurasi layanan DNS.

[SCREENSHOT 03]
Nama file: 03-dns-record-a-aaaa.png
Caption: Memeriksa A record dan AAAA record untuk mengetahui alamat IPv4 dan IPv6.
Alt text: Hasil DNS lookup A record dan AAAA record domain google.com.

### D. Memeriksa MX Record

Berikutnya, kita akan melihat informasi server email menggunakan MX record.

Jalankan perintah:

```powershell
nslookup -type=MX gmail.com
```

Hasil pemeriksaan menampilkan beberapa mail server beserta nilai preference masing-masing.

Sebagai contoh, output menampilkan server `gmail-smtp-in.l.google.com` dengan preference 5. Terdapat juga server alternatif dengan nilai preference yang lebih besar.

Perlu diingat bahwa angka preference yang lebih kecil menunjukkan prioritas yang lebih tinggi. Oleh karena itu, mail server dengan nilai preference 5 memiliki prioritas lebih tinggi dibandingkan server dengan nilai 10 atau 20.

[SCREENSHOT 04]
Nama file: 04-dns-record-mx.png
Caption: Melihat daftar mail server dan nilai preference melalui MX record.
Alt text: Hasil pemeriksaan MX record domain gmail.com menggunakan nslookup.

### E. Memeriksa NS Record

Untuk mengetahui nameserver yang digunakan oleh suatu domain, kita dapat menjalankan:

```powershell
nslookup -type=NS cloudflare.com
```

Hasilnya menampilkan beberapa nameserver, seperti `ns7.cloudflare.com`, `ns6.cloudflare.com`, dan nameserver lainnya.

Informasi tersebut menunjukkan nameserver yang tercatat untuk domain `cloudflare.com`.

Dengan memeriksa NS record, kita dapat mengetahui server DNS yang berwenang memberikan informasi DNS untuk suatu domain.

[SCREENSHOT 05A]
Nama file: 05a-dns-record-ns.png
Caption: Memeriksa daftar nameserver domain cloudflare.com menggunakan NS record.
Alt text: Hasil DNS lookup NS record domain cloudflare.com.

### F. Memeriksa TXT Record

Selanjutnya, kita akan memeriksa TXT record. Record ini dapat berisi informasi verifikasi domain, kebijakan email, dan data teks lainnya.

Jalankan perintah berikut:

```powershell
Resolve-DnsName google.com -Type TXT | Select-Object -First 5
```

Pada perintah tersebut, `Resolve-DnsName` digunakan untuk mencari TXT record. Sementara itu, `Select-Object -First 5` membatasi jumlah hasil yang ditampilkan menjadi lima objek pertama.

Hasil praktik menampilkan beberapa informasi TXT, termasuk data verifikasi domain.

Pembatasan tersebut hanya mengatur jumlah hasil yang ditampilkan di PowerShell. Artinya, bukan berarti domain tersebut hanya memiliki lima TXT record.

Perlu diperhatikan juga bahwa sebagian TXT record dapat berisi token verifikasi atau informasi konfigurasi layanan. Karena itu, hindari membagikan nilai yang bersifat sensitif ketika mengambil screenshot atau memublikasikan hasil pemeriksaan.

[SCREENSHOT 05B]
Nama file: 05b-dns-record-txt.png
Caption: Memeriksa lima hasil pertama TXT record menggunakan Resolve-DnsName.
Alt text: Hasil pemeriksaan TXT record domain google.com di Windows PowerShell.

### G. Mengamati TTL DNS

Selain jenis record, kita juga dapat memeriksa TTL atau Time to Live.

TTL merupakan nilai waktu yang menentukan berapa lama informasi DNS dapat disimpan dalam cache sebelum perlu diperbarui berdasarkan kebijakan caching yang berlaku.

Untuk melihat informasi tersebut, jalankan:

```powershell
Resolve-DnsName google.com -Type A
```

Hasil praktik menampilkan kolom `TTL` dengan nilai sekitar 234 detik pada saat pemeriksaan dilakukan.

Nilai tersebut merupakan TTL yang dikembalikan pada hasil query. Dalam konteks caching, TTL umumnya berkurang seiring waktu ketika sebuah record berada di cache resolver.

Dengan demikian, TTL bukanlah durasi koneksi internet atau waktu yang dibutuhkan untuk membuka website. Nilai ini berkaitan dengan masa berlaku informasi DNS dalam cache.

[SCREENSHOT 06]
Nama file: 06-mengamati-ttl-dns.png
Caption: Mengamati nilai TTL pada hasil query A record menggunakan Resolve-DnsName.
Alt text: Hasil pemeriksaan DNS yang menampilkan kolom TTL untuk domain google.com.

## 7. Mengapa DNS Penting dalam Networking dan DevOps?

DNS merupakan salah satu komponen penting dalam infrastruktur jaringan. Hampir semua layanan berbasis internet bergantung pada DNS untuk menemukan layanan berdasarkan nama domain.

Dalam bidang networking, DNS membantu perangkat menemukan alamat layanan dan mendukung komunikasi antarsistem. Oleh sebab itu, pemeriksaan DNS sering menjadi bagian dari proses troubleshooting ketika sebuah website atau layanan tidak dapat diakses.

Sementara itu, dalam lingkungan DevOps, DNS juga memiliki peran penting. Aplikasi yang berjalan pada server, container, maupun cloud infrastructure sering menggunakan nama domain untuk mengakses layanan lain.

Contohnya, sebuah aplikasi dapat menggunakan nama domain database atau API server sebagai alamat tujuan koneksi. Jika konfigurasi DNS bermasalah, komunikasi antarlayanan juga dapat terganggu.

Selain itu, pemahaman mengenai DNS record dan TTL membantu engineer ketika melakukan konfigurasi domain, deployment aplikasi, migrasi server, maupun pengelolaan layanan cloud.

## 8. Kesimpulan

DNS atau Domain Name System merupakan sistem yang membantu perangkat menemukan informasi berdasarkan nama domain. Salah satu fungsi utamanya adalah menerjemahkan nama domain menjadi alamat IP agar perangkat dapat berkomunikasi dengan server tujuan.

Melalui praktik menggunakan Windows PowerShell, kita telah mempelajari cara melakukan DNS lookup dengan `nslookup` dan `Resolve-DnsName`. Kita juga telah memeriksa beberapa jenis DNS record, yaitu A, AAAA, MX, NS, dan TXT, serta mengamati nilai TTL.

Dengan memahami konsep dasar DNS dan cara melakukan pemeriksaannya, kita memiliki bekal untuk melakukan troubleshooting jaringan maupun mengelola layanan dalam lingkungan DevOps.

## Referensi

1. Cloudflare Learning Center – What is DNS?
   https://www.cloudflare.com/learning/dns/what-is-dns/

2. Microsoft Learn – Resolve-DnsName
   https://learn.microsoft.com/en-us/powershell/module/dnsclient/resolve-dnsname

3. Google Public DNS – Using Google Public DNS
   https://developers.google.com/speed/public-dns/docs/using

4. RFC 1034 – Domain Names: Concepts and Facilities
   https://www.rfc-editor.org/rfc/rfc1034

5. RFC 1035 – Domain Names: Implementation and Specification
   https://www.rfc-editor.org/rfc/rfc1035
