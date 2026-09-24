# Penetration Testing Assessment Report

## 1. Informasi Assessment

| Item                    | Detail                                    |
| ----------------------- | ----------------------------------------- |
| Assessment              | Authorized PKL Penetration Testing        |
| Target utama            | `192.168.56.7`                            |
| Network scope           | `192.168.56.0/24`                         |
| Assessment host         | `192.168.56.105`                          |
| Environment             | Replicated laboratory VM / authorized lab |
| Assessment type         | Network & vulnerability assessment        |
| Status                  | Ongoing                                   |
| Vulnerability confirmed | None as of current phase                  |

> **Note:** Assessment dilakukan pada lingkungan lab/replica yang diberikan untuk kebutuhan PKL. Pengujian difokuskan pada discovery, vulnerability assessment, dan validasi non-destructive.

---

# 2. Tujuan

Assessment dilakukan untuk:

1. Mengidentifikasi host aktif dalam jaringan lab.
2. Mengidentifikasi port dan service yang terbuka.
3. Mengidentifikasi konfigurasi keamanan SMB/RPC.
4. Memeriksa vulnerability yang dapat diidentifikasi dari network layer.
5. Mencari keberadaan aplikasi web yang berpotensi menjadi target pengujian.
6. Menentukan attack surface yang dapat divalidasi lebih lanjut.
7. Menyimpan evidence setiap tahap assessment untuk kebutuhan dokumentasi PKL.

---

# 3. Scope

Network yang digunakan dalam assessment:

```text
192.168.56.0/24
```

Target utama:

```text
192.168.56.7
```

Execution / assessment VM:

```text
192.168.56.105
```

Assessment dilakukan melalui koneksi SSH dari CentOS ke assessment VM dan eksekusi command menggunakan custom `lab_exec`.

---

# 4. Methodology

Assessment dilakukan secara bertahap:

```text
Scope Verification
       ↓
Host Discovery
       ↓
Port Discovery
       ↓
Service Detection
       ↓
OS Fingerprinting
       ↓
SMB/RPC Assessment
       ↓
Vulnerability Assessment
       ↓
Vulnerability Validation
       ↓
Web Application Discovery
       ↓
Attack Surface Mapping
       ↓
PoC Validation
       ↓
Final Report
```

Pada fase saat ini, assessment belum masuk ke tahap exploit/PoC karena belum ditemukan vulnerability yang memenuhi kriteria untuk divalidasi.

---

# 5. Host Discovery

Network discovery dilakukan terhadap:

```text
192.168.56.0/24
```

Beberapa metode discovery digunakan untuk mengurangi kemungkinan false negative:

* ICMP host discovery
* TCP SYN/ACK probes
* Top TCP ports
* ARP/neighbour information

## Hasil

Host yang teridentifikasi aktif:

| IP               | Identifikasi         | Status |
| ---------------- | -------------------- | ------ |
| `192.168.56.7`   | Windows target       | Active |
| `192.168.56.105` | Alpine assessment VM | Active |

Tidak ditemukan host ketiga yang aktif pada network segment tersebut.

Evidence:

```text
raw/web-discovery/step01-host-alive-basic.txt
raw/web-discovery/step02-host-alive-extended.txt
raw/web-discovery/step03-top100-tcp-syn.txt
raw/web-discovery/step05-arp-neigh-hostonly.txt
```

---

# 6. Target `192.168.56.7`

## 6.1 OS Fingerprint

Network fingerprint mengindikasikan:

```text
Windows 11 24H2
```

Fingerprint tersebut diperlakukan sebagai indikasi network-level, bukan bukti exact build atau patch level.

Exact Windows build dan installed KB belum dapat ditentukan secara anonymous.

---

# 7. TCP Port Discovery

Full TCP discovery terhadap `192.168.56.7` menghasilkan 12 port TCP yang terverifikasi terbuka.

|  Port | Service / Detection   | Status |
| ----: | --------------------- | ------ |
|   135 | MSRPC                 | Open   |
|   139 | NetBIOS/SMB           | Open   |
|   445 | Microsoft-DS/SMB      | Open   |
|  5040 | TCP wrapped / unknown | Open   |
|  7680 | Unknown / softmatch   | Open   |
| 49664 | MSRPC                 | Open   |
| 49665 | MSRPC                 | Open   |
| 49668 | MSRPC                 | Open   |
| 49669 | MSRPC                 | Open   |
| 49670 | MSRPC                 | Open   |
| 49680 | MSRPC                 | Open   |
| 49683 | MSRPC                 | Open   |

Port lainnya teridentifikasi sebagai closed pada full TCP assessment.

Evidence:

```text
raw/full-network-assessment/step09-full-tcp.txt
raw/full-network-assessment/step09b-highports-sv.txt
raw/verified-port-inventory.md
```

---

# 8. SMB Security Assessment

Port:

```text
139/tcp
445/tcp
```

SMB dialect yang tersedia mencakup SMB 2.x dan SMB 3.x.

Temuan keamanan:

### SMBv1

```text
Disabled / Not offered
```

Tidak ditemukan SMBv1 pada negotiation.

### SMB Signing

```text
Enabled and Required
```

### Anonymous SMB

Anonymous/null session tidak berhasil digunakan untuk mendapatkan SMB session.

Validasi SMB2 signed anonymous menghasilkan:

```text
STATUS_USER_SESSION_DELETED
0xC0000203
```

Hal tersebut menunjukkan bahwa anonymous SMB session tidak dapat digunakan untuk enumeration sebagaimana yang diuji.

Evidence:

```text
raw/comprehensive-assessment/step11-smb2-signed-anonymous.txt
raw/validation/val_smb_anon_enum.txt
```

---

# 9. RPC Assessment

Port:

```text
135/tcp
49664+
```

Port 135 teridentifikasi sebagai Microsoft RPC Endpoint Mapper.

Dynamic RPC ports juga terbuka pada beberapa port:

```text
49664
49665
49668
49669
49670
49680
49683
```

Anonymous RPC enumeration tidak berhasil memperoleh mapping endpoint lengkap.

Dengan demikian:

```text
RPC attack surface = Confirmed
RPC vulnerability = Not confirmed
```

Evidence:

```text
raw/comprehensive-assessment/step12-epm-rpc-enum.txt
raw/validation/val_135_rpc.txt
raw/validation/val_135_version_trace.txt
```

---

# 10. Port 5040 dan 7680

Dua port berikut ditemukan:

```text
5040/tcp
7680/tcp
```

Keduanya menerima koneksi tetapi tidak memberikan banner yang cukup untuk memastikan identitas service dari network layer.

Beberapa fingerprint menghubungkan port tersebut dengan kemungkinan Windows services, tetapi korelasi tersebut **belum dianggap sebagai identifikasi service yang terkonfirmasi**.

Status:

| Port | Status                     |
| ---: | -------------------------- |
| 5040 | Open, identity unconfirmed |
| 7680 | Open, identity unconfirmed |

Tidak dilakukan exploit terhadap kedua service tersebut.

Evidence:

```text
raw/validation/val_5040_7680_banner_sV.txt
raw/validation/val_5040_7680_probes.txt
raw/full-network-assessment/step08-5040-7680-fingerprint.txt
```

---

# 11. Vulnerability Assessment

Beberapa vulnerability SMB/Windows legacy diperiksa secara non-destructive.

## MS17-010 / EternalBlue

```text
Not confirmed
```

SMBv1 tidak aktif sehingga attack path legacy tersebut tidak tersedia melalui konfigurasi yang ditemukan.

## MS08-067

```text
Not confirmed
```

## MS10-054

```text
Not confirmed
```

## MS10-061

```text
Not confirmed
```

## SMBGhost — CVE-2020-0796

```text
Not confirmed
```

Exact Windows build dan patch state tidak tersedia sehingga vulnerability yang bergantung pada build tertentu tidak dapat dinyatakan vulnerable hanya berdasarkan OS fingerprint.

---

# 12. Web Application Discovery

Setelah infrastructure assessment selesai, dilakukan discovery terhadap network:

```text
192.168.56.0/24
```

Hasil host discovery menunjukkan hanya:

```text
192.168.56.7
192.168.56.105
```

Tidak ditemukan host lain yang aktif.

Pada target Windows:

```text
192.168.56.7
```

tidak ditemukan HTTP/HTTPS service pada port yang teridentifikasi.

Dengan demikian, enam kategori vulnerability web yang sebelumnya diduga belum dapat diuji:

1. Broken Access Control / IDOR
2. SQL Injection
3. Reflected XSS
4. Insecure File Upload
5. Weak Session Management
6. Information Disclosure

Status:

```text
Web application target = Not Found
Web vulnerability = Not Assessed
```

Evidence:

```text
raw/web-discovery/
findings/web-discovery.md
```

---

# 13. Assessment VM Service Observation

Pada `192.168.56.105`, observasi socket lokal menunjukkan beberapa listening service:

```text
TCP 22
TCP 3000
TCP 3307
```

Port tersebut belum dianggap sebagai target assessment karena `192.168.56.105` digunakan sebagai assessment/execution VM dan scope aplikasi pada host tersebut belum dikonfirmasi.

Khusus:

```text
192.168.56.105:3000
192.168.56.105:3307
```

dapat menjadi kandidat investigation berikutnya apabila host tersebut memang termasuk scope resmi dari environment yang diberikan industri.

Tidak ada vulnerability yang diklaim berdasarkan observasi tersebut.

---

# 14. Confirmed Security Properties

Assessment berhasil mengkonfirmasi beberapa security properties:

### Positive security controls

* SMBv1 tidak tersedia.
* SMB signing required.
* Anonymous SMB session ditolak.
* Legacy SMB vulnerability paths tidak terkonfirmasi.

### Exposed attack surface

* Microsoft RPC Endpoint Mapper.
* Dynamic RPC ports.
* SMB/NetBIOS.
* TCP 5040.
* TCP 7680.
* UDP 137.

Exposed service tidak secara otomatis berarti vulnerability.

---

# 15. Vulnerability Status

| Vulnerability          | Status                              | Reason                         |
| ---------------------- | ----------------------------------- | ------------------------------ |
| MS17-010               | Not confirmed                       | SMBv1 unavailable              |
| MS08-067               | Not confirmed                       | No vulnerable path established |
| MS10-054               | Not confirmed                       | No vulnerable path established |
| MS10-061               | Not confirmed                       | No vulnerable path established |
| SMBGhost               | Not confirmed                       | Exact build/patch unavailable  |
| Anonymous SMB          | Not vulnerable based on tested path | Anonymous session rejected     |
| RPC exposure           | Attack surface only                 | No vulnerability confirmed     |
| Web IDOR               | Not assessed                        | Web application not found      |
| SQL Injection          | Not assessed                        | Web application not found      |
| Reflected XSS          | Not assessed                        | Web application not found      |
| File Upload            | Not assessed                        | Web application not found      |
| Session Management     | Not assessed                        | Web application not found      |
| Information Disclosure | Not assessed                        | Web application not found      |

---

# 16. PoC Status

```text
PoC candidates: NONE
```

Tidak ada PoC yang dijalankan pada fase ini.

Alasannya:

```text
Discovery
    ↓
No confirmed vulnerability
    ↓
No valid PoC target
```

Hal ini mencegah pengujian eksploitatif yang tidak memiliki dasar vulnerability yang jelas.

---

# 17. Remaining Gaps

Beberapa informasi masih belum dapat diperoleh dari network-level anonymous assessment:

### G-1 — Exact Windows Build / Patch Level

Diperlukan untuk memastikan vulnerability yang bergantung pada build dan patch tertentu.

### G-3 — RPC Endpoint Mapping

UUID-to-service mapping lengkap belum dapat diperoleh secara anonymous.

### G-4 — Service Identity

Identitas proses untuk:

```text
5040/tcp
7680/tcp
```

belum dapat dipastikan dari network layer.

### G-6 — RPC Endpoint ACL

Access control endpoint RPC belum dapat divalidasi tanpa akses yang sesuai.

### Web Application Scope

Belum diketahui apakah terdapat VM/aplikasi web lain yang seharusnya termasuk dalam lab scope.

---

# 18. Evidence Structure

Evidence assessment disimpan dalam struktur:

```text
pentest-192.168.56.7/
├── scope.md
├── findings/
│   ├── vulnerability-assessment.md
│   ├── vulnerability-validation.md
│   ├── network-vulnerability-assessment-v2.md
│   ├── correlation-analysis.md
│   ├── verified-port-inventory.md
│   ├── comprehensive-vulnerability-assessment.md
│   └── web-discovery.md
│
├── raw/
│   ├── full-network-assessment/
│   ├── validation/
│   ├── comprehensive-assessment/
│   └── web-discovery/
│
└── reports/
```

Raw output dipisahkan dari findings agar evidence asli tetap tersedia dan laporan dapat dibaca tanpa harus membuka seluruh output scanner.

---

# 19. Current Conclusion

Berdasarkan assessment sampai fase web discovery:

> **Tidak ditemukan vulnerability yang dapat dikonfirmasi pada `192.168.56.7` berdasarkan network-level testing yang telah dilakukan.**

Target memiliki SMB/RPC attack surface yang cukup jelas, tetapi kontrol seperti SMBv1 disabled, SMB signing required, dan anonymous SMB rejection berhasil dikonfirmasi.

Tidak ditemukan web application pada network segment `192.168.56.0/24` selain service yang berjalan pada assessment VM `192.168.56.105`, yang status scope-nya belum dikonfirmasi.

Oleh karena itu, pengujian terhadap:

```text
IDOR
SQL Injection
Reflected XSS
Insecure File Upload
Weak Session Management
Information Disclosure
```

belum dilakukan dan **tidak boleh dianggap sebagai vulnerability yang tidak ada**. Status yang tepat adalah **Not Assessed / No Web Target Found**.

---

# 20. Recommended Next Assessment

Sebelum melakukan pengujian web lebih lanjut, scope environment perlu dikonfirmasi.

Jika:

```text
192.168.56.105:3000
192.168.56.105:3307
```

merupakan bagian dari target resmi, assessment berikutnya dapat berfokus pada identifikasi service dan aplikasi tersebut.

Jika bukan, diperlukan VM/web server lain dari environment industri.

Tahap berikutnya setelah web application ditemukan:

```text
Web Fingerprinting
        ↓
Endpoint Mapping
        ↓
Parameter
```
