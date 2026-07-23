# Daily Report - Day 3

**Tanggal:** 22 Juli 2026

## Ringkasan

Melakukan persiapan environment Debian 13 sebagai server utama untuk kegiatan PKL. Fokus pekerjaan hari ini adalah konfigurasi jaringan, pembaruan sistem, aktivasi akses remote, serta instalasi layanan DNS Server sebagai persiapan proyek berikutnya.

---

## Aktivitas

### 1. Konfigurasi Network
- Mengonfigurasi VirtualBox menggunakan NAT dan Host-Only Adapter.
- Melakukan troubleshooting routing dan default gateway.
- Memastikan koneksi internet berjalan dengan baik.

### 2. Pengujian Konektivitas
- Menguji koneksi ke gateway.
- Menguji koneksi ke host.
- Menguji koneksi ke internet menggunakan `ping`.

### 3. Konfigurasi SSH
- Memastikan layanan OpenSSH berjalan.
- Melakukan pengujian remote server menggunakan PuTTY.

### 4. System Update
- Melakukan pembaruan sistem menggunakan `apt update` dan `apt full-upgrade`.
- Menyelesaikan konfigurasi GRUB setelah proses upgrade.

### 5. Instalasi DNS Server
- Menginstal paket:
  - bind9
  - bind9-utils
  - bind9-doc
  - dnsutils
- Memastikan service BIND9 berjalan dengan baik.
- Melakukan pengecekan port DNS (53).

---

## Kendala

- Terjadi konflik default gateway yang menyebabkan server tidak dapat mengakses internet.
- Permasalahan berhasil diidentifikasi dan diselesaikan dengan menghapus default gateway pada interface Host-Only.

---

## Hasil

- Debian 13 berhasil dikonfigurasi.
- Koneksi internet telah berfungsi normal.
- SSH dapat diakses menggunakan PuTTY.
- Sistem berhasil diperbarui.
- BIND9 berhasil diinstal dan berjalan dengan status **active (running)**.

---

## Rencana Selanjutnya

- Melakukan konfigurasi DNS Server (BIND9).
- Membuat Forward Zone dan Reverse Zone.
- Melakukan pengujian DNS menggunakan `dig` dan `nslookup`.
- Menyusun dokumentasi proyek DNS Server.
