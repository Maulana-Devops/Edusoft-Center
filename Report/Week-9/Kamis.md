
# FIT ITS — Assessment & Pentest Report

## 1. Overview

Assessment ini dilakukan terhadap aplikasi `FIT_ITS` yang diberikan untuk keperluan evaluasi sistem existing sebelum proses pengembangan/upgrade aplikasi baru.

Tujuan assessment:

- Memahami arsitektur dan teknologi aplikasi existing.
- Mengidentifikasi struktur database dan alur fungsional aplikasi.
- Memetakan mekanisme authentication dan authorization.
- Mengidentifikasi penggunaan file system dan executable eksternal.
- Mengidentifikasi area yang perlu diuji lebih lanjut dari sisi keamanan.
- Menjadi dasar penyusunan requirement untuk aplikasi pengganti/upgrade.

Assessment dilakukan pada working copy agar tidak mengubah data/source package asli.

---

## 2. Scope

Package yang dianalisis:

```text
FIT_ITS.rar
````

Working directory:

```text
~/Downloads/FIT_ITS-pentest
```

Analisis mencakup:

* `ITS.EXE`
* File database `.DBF`
* File index `.CDX`
* File konfigurasi `.INI` dan `.MEM`
* `XPRINT.EXE`
* `7ZA`
* Static strings dan symbol pada executable
* Struktur authentication
* Struktur authorization
* Struktur menu/program
* Operasi backup/restore/reset/reindex
* Referensi filesystem dan external execution

Catatan:

Database yang tersedia pada package assessment bukan merupakan representasi penuh dari database production. Sebagian tabel transaksi kosong atau hanya memiliki sedikit record.

---

# 3. Existing Application Identification

Aplikasi yang ditemukan pada package teridentifikasi sebagai:

```text
EZSOFT Integrated Trading System (ITS)
Version : 3.20
Author  : Julian Aristo
Manual  : November 2018
```

Executable utama:

```text
ITS.EXE
```

Karakteristik teknis:

```text
Platform       : Windows
Architecture   : 32-bit
Executable     : PE32
Runtime/Compiler: Harbour / xBase / Clipper compatible
Database       : DBF
Index          : CDX
```

Tidak ditemukan source code aplikasi dalam package yang dianalisis.

Beberapa nama module `.PRG` masih terdapat sebagai metadata/symbol di dalam executable, antara lain:

```text
C_USER.PRG
C_RESET.PRG
C_BARANG.PRG
C_GRUP.PRG
C_GRUPC.PRG
C_7ZA.PRG
```

Hal tersebut membantu proses reverse engineering, tetapi tidak berarti source code asli berhasil dipulihkan.

---

# 4. Database Architecture

Aplikasi menggunakan database berbasis DBF dengan index CDX.

Database yang ditemukan:

| Database     | Indikasi fungsi           |
| ------------ | ------------------------- |
| `PASS.DBF`   | Authentication / user     |
| `PROG.DBF`   | Program / menu permission |
| `SETUP.DBF`  | System configuration      |
| `BARANG.DBF` | Product / inventory       |
| `GRUP.DBF`   | Product group             |
| `CUST.DBF`   | Customer                  |
| `SUPP.DBF`   | Supplier                  |
| `SALES.DBF`  | Salesman                  |
| `JUAL.DBF`   | Sales transaction         |
| `JUALT.DBF`  | Sales transaction detail  |
| `PIUT.DBF`   | Accounts receivable       |
| `HUTA.DBF`   | Accounts payable          |
| `PBAYAR.DBF` | Receivable payment        |
| `HBAYAR.DBF` | Payable payment           |

Index database menggunakan file `.CDX`, misalnya:

```text
BARANG.CDX
CUST.CDX
GRUP.CDX
JUAL.CDX
JUALT.CDX
PIUT.CDX
HUTA.CDX
PBAYAR.CDX
HBAYAR.CDX
```

---

# 5. Database Inventory

Jumlah record yang teridentifikasi pada package assessment:

```text
BARANG.DBF   : 27 records
CUST.DBF     : 66 records
SUPP.DBF     : 1 record
SALES.DBF    : 3 records
GRUP.DBF     : 1 record

JUAL.DBF     : 3 records
JUALT.DBF    : 0 records
PIUT.DBF     : 0 records
HUTA.DBF     : 0 records
PBAYAR.DBF   : 0 records
HBAYAR.DBF   : 0 records
```

Kesimpulan:

Database yang diberikan kemungkinan merupakan sample/working database dan belum dapat dianggap sebagai full production dataset.

---

# 6. Authentication Findings

Static analysis menemukan module dan function yang berkaitan dengan authentication:

```text
CHKUSER
BUATUSER
BUKAPROG
C_USER.PRG
_HB_FUN_CHKUSER
_HB_FUN_BUATUSER
```

String authentication yang ditemukan:

```text
Nama User :
Password :
Nama User tidak ada !
```

File authentication:

```text
PASS.DBF
```

Struktur `PASS.DBF`:

```text
NAMA
PASS
PASS2
PASS3
PASS4
PASS5
```

User yang teridentifikasi pada sample database:

```text
SPV
JULIAN
```

### Current assessment status

```text
Authentication mechanism : Confirmed
User database            : Confirmed
Login validation         : Indicated
Authentication security  : Requires dynamic testing
```

Credential/password tidak dimasukkan ke dalam laporan untuk menghindari disclosure informasi authentication.

---

# 7. Authorization Findings

Authorization menggunakan file:

```text
PROG.DBF
```

Struktur:

```text
Records       : 84
Header length : 129 bytes
Record length : 57 bytes
```

Fields:

```text
FLDNILAI : Character(5)
FLDOK    : Character(1)
FLDNAMA  : Character(50)
```

Contoh permission/program yang ditemukan:

```text
PW1  → Pendataan Barang
PW61 → Lihat Data Barang
PW2  → Cetak Daftar Barang
PW82 → Cetak Daftar Barang Per Grup Barang
PW53 → Pendataan Grup Barang
PW54 → Cetak Daftar Grup Barang
PW3  → Pendataan Customer
PW4  → Cetak Daftar Customer
PW5  → Pendataan Supplier
PW6  → Cetak Daftar Supplier
PW7  → Pendataan Salesman
PW8  → Cetak Daftar Salesman
PW9  → Pendataan Penjualan Barang
PW10 → Pendataan Retur Penjualan Barang
PW11 → Pendataan Pembelian Barang
PW12 → Pendataan Retur Pembelian Barang
PW13 → Pendataan Masuk Lain-Lain
PW14 → Pendataan Keluar Lain-Lain
PW15 → Pendataan Piutang
PW16 → Pendataan Pembayaran Piutang
```

Static analysis juga menemukan:

```text
Set Menu User (Y/T) ?
PEMBUATAN USER
BUKAPROG
PROG
```

### Assessment

Sistem memiliki mekanisme permission yang cukup granular pada level program/menu.

Namun, static analysis belum membuktikan apakah permission tersebut:

1. hanya digunakan untuk menampilkan/menyembunyikan menu, atau
2. benar-benar divalidasi pada level function/business logic.

Hal tersebut menjadi target dynamic testing berikutnya.

---

# 8. Functional Scope Identified

Berdasarkan menu dan string pada executable, existing application memiliki beberapa area bisnis.

## Master Data

```text
Barang
Grup Barang
Customer
Supplier
Salesman
```

## Transaction

```text
Penjualan Barang
Retur Penjualan
Pembelian Barang
Retur Pembelian
Masuk Lain-Lain
Keluar Lain-Lain
Piutang
Hutang
Pembayaran Piutang
Pembayaran Hutang
```

## Reporting

Ditemukan referensi terhadap:

```text
Inventory
Pembelian
Penjualan
Retur
Komisi Salesman
Gross Profit
Piutang
Hutang
Umur Piutang
Umur Hutang
Jatuh Tempo
Pembayaran
```

Hal ini menunjukkan bahwa existing system mencakup proses master data, inventory, sales, purchasing, account receivable, account payable, dan reporting.

---

# 9. Backup & Restore

Static analysis menemukan module backup/restore:

```text
Backup dan Restore Data
Backup
Restore
Backup Data ke =>
Restore Data dari =>
Backup (Y/T) ?
Restore (Y/T) ?
Backup selesai !
Restore selesai !
```

Aplikasi juga memiliki referensi terhadap:

```text
7ZA
BR7ZA
C_7ZA.PRG
```

Hal tersebut menunjukkan penggunaan executable eksternal untuk proses archive/backup/restore.

### Security assessment status

```text
Backup functionality        : Confirmed
Restore functionality       : Confirmed
External archive utility    : Confirmed
Backup authorization        : Requires dynamic testing
Restore authorization       : Requires dynamic testing
Path validation             : Requires dynamic testing
```

Pengujian destruktif terhadap data tidak dilakukan.

---

# 10. Database Reset

Static analysis menemukan:

```text
RESET DATABASE
```

dengan pilihan:

```text
1. Reset Semua
2. Reset Semua Kecuali Master
```

Module yang berkaitan:

```text
C_RESET.PRG
RESET
DBDELETE
FERASE
```

### Assessment status

```text
Reset functionality : Confirmed
Database deletion    : Indicated
Access control       : Requires dynamic testing
```

Fungsi reset tidak dijalankan pada production data.

---

# 11. Reindex

Ditemukan functionality:

```text
Reindex Data (Y/T) ?
Reindex Data Selesai !
```

serta symbol:

```text
DBREINDEX
_HB_FUN_DBREINDEX
```

Hal ini konsisten dengan penggunaan DBF/CDX sebagai database engine.

---

# 12. External Process Execution

Static analysis menemukan:

```text
RUNWIN
RUNPDF
SWPRUNCMD
HB_RUN
COMSPEC
_wsystem
```

External executable yang direferensikan:

```text
XPRINT.EXE
7ZA
```

Contoh command reference:

```text
XPRINT.EXE /LEFT 0.5 /SEL /FOCUS
XPRINT.EXE /PDF /FOCUS REPORT
```

### Assessment

Existing application memiliki mekanisme untuk menjalankan proses eksternal.

Namun keberadaan `RUNWIN`, `SWPRUNCMD`, atau `HB_RUN` sendiri belum cukup untuk menyimpulkan adanya command injection.

Masih diperlukan analisis terhadap sumber parameter dan bagaimana command dibentuk sebelum dapat menentukan risiko keamanan.

---

# 13. File System Operations

Static analysis menemukan penggunaan operasi:

```text
COPY
FERASE
DELETE
DBDELETE
HB_FCOPY
HB_DIRDELETE
HB_DBRENAME
DBREINDEX
```

Juga ditemukan Windows API:

```text
DeleteFileW
```

### Assessment

Aplikasi memiliki capability untuk melakukan operasi file/database.

Namun belum ditemukan bukti bahwa user dapat mengontrol arbitrary filesystem path.

Pengujian path handling dan authorization masih diperlukan pada dynamic testing.

---

# 14. Configuration Files

File konfigurasi yang ditemukan:

```text
ADMSYS.INI
ADMPATH.MEM
SETUP.DBF
SETUP.MEM
```

`ADMPATH.MEM` menjadi file yang perlu diperhatikan karena berpotensi menentukan lokasi/path database.

Konfigurasi perusahaan juga ditemukan pada database/configuration package.

Informasi sensitif seperti credential dan data authentication tidak dimasukkan dalam repository publik.

---

# 15. Static Analysis Methodology

Analisis awal dilakukan menggunakan beberapa teknik:

```text
File inventory
DBF structure parsing
Binary strings extraction
Keyword analysis
Executable symbol analysis
Database reference analysis
Authentication reference analysis
Authorization reference analysis
File operation analysis
External command reference analysis
```

Contoh command yang digunakan:

```bash
strings -a -n 4 ITS.EXE
```

Kemudian dilakukan filtering terhadap keyword:

```text
LOGIN
PASSWORD
USER
CHKUSER
BUATUSER
PROG
BACKUP
RESTORE
RESET
REINDEX
RUNWIN
RUNPDF
XPRINT
7ZA
```

Analisis database dilakukan dengan membaca header DBF dan field descriptor tanpa memodifikasi data.

---

# 16. Security Finding Status

Pada tahap static analysis, hasil diklasifikasikan sebagai berikut:

| Area                            | Status           |
| ------------------------------- | ---------------- |
| Legacy application architecture | Confirmed        |
| DBF/CDX database                | Confirmed        |
| Authentication mechanism        | Confirmed        |
| User management                 | Confirmed        |
| Program/menu permission         | Confirmed        |
| Backup functionality            | Confirmed        |
| Restore functionality           | Confirmed        |
| Database reset                  | Confirmed        |
| Database reindex                | Confirmed        |
| External executable execution   | Confirmed        |
| File operation capability       | Confirmed        |
| Authentication bypass           | Not yet verified |
| Authorization bypass            | Not yet verified |
| Command injection               | Not yet verified |
| Arbitrary file access           | Not yet verified |
| Path traversal                  | Not yet verified |
| Weak password policy            | Not yet verified |
| Function-level authorization    | Not yet verified |

`Confirmed` pada tabel di atas berarti functionality/structure berhasil diidentifikasi dari package. Hal tersebut tidak otomatis berarti functionality tersebut merupakan vulnerability.

---

# 17. Preliminary Architecture Map

```text
                         ITS.EXE
                            │
        ┌───────────────────┼────────────────────┐
        │                   │                    │
 Authentication       Authorization         Business Logic
        │                   │                    │
    PASS.DBF            PROG.DBF                │
        │                   │                    │
    CHKUSER          Program/Menu              │
    BUATUSER          Permission                │
        │                   │                    │
        └───────────────────┼────────────────────┘
                            │
                     DBF/CDX Database
                            │
       ┌────────────────────┼────────────────────┐
       │                    │                    │
   Master Data         Transactions          Reporting
       │                    │                    │
   BARANG              JUAL/JUALT           Inventory
   GRUP                PIUT                 Sales
   CUST                HUTA                 Purchase
   SUPP                PBAYAR               AR/AP
   SALES               HBAYAR               Profit
       │                    │
       └────────────────────┼────────────────────┘
                            │
                  System Maintenance
                            │
            ┌───────────────┼───────────────┐
            │               │               │
         Backup          Restore          Reset
            │               │               │
           7ZA             7ZA          DBDELETE
                                            │
                                        Reindex
                                            │
                                       DBREINDEX

External Process:
ITS.EXE → XPRINT.EXE
ITS.EXE → 7ZA
```

---

# 18. Next Assessment Plan

Tahap berikutnya adalah dynamic assessment menggunakan working copy dan credential yang diberikan secara resmi oleh client.

Prioritas pengujian:

### Authentication

```text
Valid username + valid password
Valid username + invalid password
Invalid username + password
Empty username
Empty password
```

### Authorization

Membandingkan akses user yang tersedia terhadap:

```text
Master
Transaction
Reports
User management
Backup
Restore
Reset
Reindex
System configuration
```

Fokus utama:

> Apakah permission ditegakkan pada level function atau hanya pada level menu.

### Input Validation

Pengujian akan difokuskan pada field input aplikasi dengan metode non-destructive.

### File Operations

Validasi:

```text
Backup path
Restore path
Generated files
Report output
Access control
```

### External Execution

Menganalisis bagaimana:

```text
RUNWIN
RUNPDF
SWPRUNCMD
```

menerima dan membentuk parameter.

Pengujian command injection hanya dilakukan apabila terdapat indikasi bahwa input user dapat mencapai command execution boundary.

---

# 19. Assessment Conclusion — Current Stage

Assessment awal menunjukkan bahwa FIT ITS merupakan aplikasi desktop legacy berbasis Harbour/xBase dengan database DBF/CDX.

Aplikasi memiliki cakupan bisnis yang cukup luas, meliputi:

```text
Master Data
Inventory
Sales
Purchase
Accounts Receivable
Accounts Payable
Reporting
Backup/Restore
System Maintenance
User Management
```

Dari sisi security architecture, area yang paling membutuhkan validasi lanjutan adalah:

```text
Authentication
Authorization
Backup/Restore access control
Reset access control
Input validation
File/path handling
External process execution
```

Pada tahap ini belum ditetapkan vulnerability final untuk area yang masih berstatus `Not yet verified`. Temuan tersebut akan divalidasi melalui dynamic testing pada working copy.

---

## 20. Assessment Environment

```text
Assessment OS : CentOS Stream 10
Runtime       : Wine
Target        : FIT ITS v3.20
Assessment    : Static Analysis + Planned Dynamic Testing
Environment   : Isolated Working Copy
Original Data : Not modified
```

---

## 21. Evidence Directory

Evidence dan hasil analisis disimpan dalam:

```text
pentest/static/
```

File hasil analisis yang telah dibuat:

```text
strings.txt
flow-keywords.txt
file-references.txt
database-references.txt
authorization-flow.txt
command-execution.txt
file-operations.txt
```

---

## Status

```text
[✓] Package inventory
[✓] Application identification
[✓] Binary identification
[✓] Database identification
[✓] Database structure analysis
[✓] Authentication mapping
[✓] Authorization mapping
[✓] Business function mapping
[✓] Backup/restore mapping
[✓] Reset/reindex mapping
[✓] External execution mapping
[ ] Complete authorization matrix
[ ] Dynamic authentication testing
[ ] Dynamic authorization testing
[ ] Input validation testing
[ ] File/path security testing
[ ] Final vulnerability classification
[ ] Final remediation recommendation
```

> Assessment ini merupakan preliminary technical assessment. Vulnerability classification dan severity hanya diberikan setelah temuan dapat divalidasi melalui evidence yang memadai.

```

**Catatan untuk GitHub:** jangan upload `PASS.DBF`, credential, password, database production, atau file konfigurasi yang mengandung secret. Untuk repository industri, lebih aman memasukkan laporan ini + evidence yang sudah disanitasi.
```
