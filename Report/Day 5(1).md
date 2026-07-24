LAPORAN HARIAN PKL
Day 5 - Output 2
Implementasi PHP-FPM dan Integrasi dengan Nginx

Hari/Tanggal : Jumat, 24 Juli 2026

Output : PHP-FPM Integration

Uraian Kegiatan

Setelah Database Server berhasil diimplementasikan, kegiatan dilanjutkan dengan instalasi PHP 8.4 beserta PHP-FPM (FastCGI Process Manager) pada Debian 13. PHP digunakan sebagai bahasa pemrograman server-side untuk membangun website dinamis, sedangkan PHP-FPM berfungsi sebagai penghubung antara web server Nginx dengan interpreter PHP.

Tahap pertama dilakukan instalasi paket PHP beserta beberapa modul pendukung seperti php-mysql, php-cli, php-curl, php-mbstring, php-xml, dan php-zip. Setelah proses instalasi selesai, dilakukan pengecekan versi PHP serta memastikan service php8.4-fpm berjalan dengan normal.

Selanjutnya dilakukan konfigurasi pada web server Nginx dengan mengaktifkan pemrosesan file PHP menggunakan Unix Socket php8.4-fpm.sock. Setelah konfigurasi selesai, dilakukan pengujian konfigurasi Nginx menggunakan perintah nginx -t untuk memastikan tidak terdapat kesalahan konfigurasi sebelum service dijalankan kembali.

Sebagai pengujian, dibuat file info.php yang berisi fungsi phpinfo() untuk memastikan bahwa Nginx berhasil meneruskan request ke PHP-FPM. Setelah halaman PHP berhasil ditampilkan melalui browser, dilakukan pengujian koneksi ke database dengan membuat file database.php menggunakan fungsi mysqli_connect(). Pengujian berhasil menunjukkan bahwa PHP dapat melakukan koneksi ke database MariaDB dengan baik.

Hasil yang Dicapai
PHP 8.4 berhasil diinstal.
PHP-FPM berhasil diinstal dan dijalankan.
Nginx berhasil dikonfigurasi untuk memproses file PHP.
Halaman phpinfo() berhasil ditampilkan melalui browser.
PHP berhasil melakukan koneksi ke database MariaDB.
Infrastruktur web telah siap dikembangkan menjadi website dinamis.
Kendala

Saat melakukan pengujian konfigurasi Nginx menggunakan perintah nginx -t, muncul pesan kesalahan:

fastcgi_pass directive is duplicate

Kesalahan tersebut disebabkan karena terdapat dua directive fastcgi_pass pada blok konfigurasi PHP di dalam file konfigurasi Nginx.

Solusi

Dilakukan pengecekan terhadap file konfigurasi Nginx dan ditemukan bahwa masih terdapat konfigurasi fastcgi_pass 127.0.0.1:9000 yang aktif bersamaan dengan konfigurasi Unix Socket php8.4-fpm.sock. Konfigurasi yang tidak digunakan kemudian dihapus sehingga hanya tersisa satu directive fastcgi_pass. Setelah dilakukan pengujian ulang menggunakan nginx -t, konfigurasi dinyatakan valid dan service Nginx berhasil dijalankan kembali.

Kesimpulan

Implementasi PHP-FPM berhasil dilakukan dengan baik. Integrasi antara Nginx, PHP-FPM, dan MariaDB telah berjalan sesuai harapan sehingga server telah siap digunakan untuk mengembangkan website portofolio dinamis berbasis PHP yang terhubung langsung dengan database MariaDB. Dengan selesainya tahap ini, infrastruktur server yang dibangun telah mencakup DNS Server, Web Server, Database Server, serta PHP Application Layer yang saling terintegrasi.
