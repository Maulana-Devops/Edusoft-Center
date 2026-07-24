Day 5 - Output 1
Implementasi Database Server (MariaDB)

Hari/Tanggal : Jumat, 24 Juli 2026

Output : Database Server (MariaDB)

Uraian Kegiatan

Pada kegiatan ini dilakukan implementasi Database Server menggunakan MariaDB sebagai media penyimpanan data untuk website portofolio yang sedang dikembangkan. Tahap awal dimulai dengan melakukan instalasi paket MariaDB Server pada sistem operasi Debian 13, kemudian memastikan service MariaDB berjalan dengan baik melalui pengecekan status service menggunakan systemctl.

Setelah proses instalasi selesai, dilakukan konfigurasi awal dengan membuat sebuah database baru bernama portfolio_db yang nantinya digunakan untuk menyimpan seluruh data website. Selanjutnya dibuat user database khusus bernama webuser serta diberikan hak akses (privileges) terhadap database tersebut agar aplikasi web tidak menggunakan akun root saat melakukan koneksi ke database.

Tahap berikutnya adalah pembuatan struktur database dengan membuat beberapa tabel, yaitu projects, skills, certificates, dan contacts. Tabel-tabel tersebut dipersiapkan sebagai penyimpanan data proyek, kemampuan yang dimiliki, sertifikat, serta data kontak yang nantinya akan ditampilkan pada website portofolio.

Sebagai pengujian, dilakukan penambahan beberapa data contoh ke dalam tabel projects, kemudian dilakukan proses pembacaan data menggunakan perintah SQL untuk memastikan seluruh proses penyimpanan dan pengambilan data berjalan dengan baik.

Hasil yang Dicapai
MariaDB Server berhasil diinstal pada Debian 13.
Database portfolio_db berhasil dibuat.
User database webuser berhasil digunakan.
Hak akses user terhadap database berhasil diberikan.
Tabel projects, skills, certificates, dan contacts berhasil dibuat.
Data berhasil ditambahkan ke dalam tabel projects.
Pengujian menggunakan perintah SELECT berhasil menampilkan data yang telah disimpan.
Kendala

Pada saat membuat user database menggunakan perintah CREATE USER, sistem menampilkan pesan:

ERROR 1396 (HY000): Operation CREATE USER failed for 'webuser'@'localhost'

Hal tersebut terjadi karena user webuser ternyata sudah pernah dibuat sebelumnya sehingga MariaDB menolak pembuatan user dengan nama yang sama.

Solusi

Dilakukan pengecekan daftar user yang tersedia pada MariaDB. Setelah diketahui bahwa user webuser telah ada, proses pembuatan user tidak dilanjutkan dan hanya dilakukan pemberian hak akses (GRANT PRIVILEGES) terhadap database portfolio_db, kemudian dilakukan FLUSH PRIVILEGES agar perubahan hak akses dapat diterapkan.

Kesimpulan

Implementasi Database Server menggunakan MariaDB berhasil dilakukan. Database telah siap digunakan sebagai backend penyimpanan data website portofolio dan dapat diakses menggunakan user khusus tanpa menggunakan akun root.
