# SIOD Development Report

**Project:** Smart Infrastructure Operations Dashboard (SIOD)
**Tanggal:** Kamis, 27 Agustus 2026
**Status:** Development & Refinement
**Tracking ID:** `SIOD-2026-08-27`

---

## 1. Ringkasan

Pada Kamis, 27 Agustus 2026, pengembangan SIOD difokuskan pada penyempurnaan sistem monitoring, khususnya pada sisi incident management, logging, Telegram notification, telemetry API, serta antarmuka dashboard.

Selain perbaikan backend, dilakukan pula perombakan tampilan dashboard menggunakan HTML dan CSS agar informasi monitoring lebih mudah dibaca dan dashboard memiliki tampilan yang lebih konsisten.

Tahap akhir pekerjaan difokuskan pada perapihan dokumentasi project dan persiapan dokumentasi video.

---

## 2. Pekerjaan yang Dilakukan

### 2.1. Audit Backend

Dilakukan pemeriksaan terhadap struktur backend SIOD dan hubungan antar-komponen monitoring.

Komponen yang diperiksa meliputi:

* `backend/main.py`
* `backend/api.py`
* `backend/incident_manager.py`
* telemetry processing
* incident analyzer
* Telegram notification
* systemd service

Tujuan audit adalah memastikan alur monitoring dari pengambilan metric hingga notification dapat berjalan secara terstruktur.

---

### 2.2. Perbaikan Incident Management

Sistem `IncidentManager` diperiksa dan diperbaiki untuk menangani lifecycle incident.

Konsep lifecycle yang digunakan:

```text
NORMAL
   ↓
THRESHOLD EXCEEDED
   ↓
ACTIVE INCIDENT
   ↓
RECOVERY
   ↓
RESOLVED
```

Pemeriksaan difokuskan pada:

* pembuatan incident
* status `ACTIVE`
* proses recovery
* status `RESOLVED`
* penyimpanan incident history
* struktur `incident_log.json`

Ditemukan pula adanya mekanisme logging pada beberapa bagian sistem yang berpotensi menghasilkan pencatatan atau notifikasi ganda.

Hal tersebut menjadi bagian dari proses refactoring agar pengelolaan incident memiliki satu alur yang lebih jelas.

---

### 2.3. Perbaikan Logging

Logging SIOD ditinjau kembali untuk memastikan aktivitas monitoring dan incident dapat ditelusuri.

Fokus perbaikan:

* pencatatan incident
* status incident
* recovery event
* Telegram notification
* systemd service log
* pemisahan antara operational log dan incident history

Salah satu masalah yang ditemukan adalah adanya komponen legacy yang masih memiliki mekanisme analyzer/logging sendiri sehingga berpotensi menyebabkan duplikasi proses.

---

### 2.4. Perbaikan Telegram Notification

Integrasi Telegram diverifikasi kembali setelah perbaikan backend.

Telegram digunakan sebagai kanal notification ketika terjadi kondisi infrastructure yang melewati threshold.

Pengujian menunjukkan bahwa notification berhasil dikirim, ditandai dengan log:

```text
[TELEGRAM SENT]
```

Monitoring notification mencakup kondisi seperti:

* CPU utilization tinggi
* memory utilization tinggi
* incident aktif
* recovery dari kondisi abnormal

Konfigurasi environment juga diperiksa agar credential Telegram dapat dibaca dengan benar oleh service systemd.

---

### 2.5. Validasi Telemetry API

Endpoint telemetry diperiksa kembali untuk memastikan data monitoring dapat dikonsumsi oleh frontend.

Endpoint yang diuji:

```text
/api/telemetry
```

Data yang diverifikasi mencakup:

* current metrics
* historical metrics
* CPU
* memory
* disk
* network
* container information

Pengujian dilakukan dengan mengambil response API secara langsung dan memeriksa struktur JSON yang dihasilkan.

---

## 3. Perombakan UI Dashboard

Setelah sisi backend dan telemetry diperiksa, pekerjaan dilanjutkan pada frontend.

File utama yang diperiksa dan diperbarui:

```text
frontend/templates/dashboard.html
frontend/static/style.css
```

Perubahan difokuskan pada:

* layout dashboard
* visual hierarchy
* metric cards
* status monitoring
* incident information
* spacing
* typography
* responsive layout
* konsistensi elemen UI

Tujuan utama redesign bukan hanya membuat dashboard terlihat lebih modern, tetapi juga meningkatkan **operational readability**, sehingga kondisi infrastructure dapat dipahami dengan cepat.

---

## 4. Hasil Perbaikan UI

Dashboard mengalami perubahan visual dibandingkan tampilan sebelumnya.

Fokus desain diarahkan pada konsep:

```text
Infrastructure Status
        ↓
Key Metrics
        ↓
System Health
        ↓
Incident Information
        ↓
Historical / Supporting Data
```

Dengan struktur tersebut, informasi yang paling penting untuk operator ditempatkan pada area yang lebih mudah ditemukan.

CSS kemudian disesuaikan kembali berdasarkan hasil visual testing pada dashboard.

---

## 5. Dokumentasi Project

Dokumentasi project juga diperiksa dan dirapikan.

Dokumentasi arsitektur monitoring disatukan ke dalam README agar informasi utama project dapat ditemukan dari satu tempat.

Arsitektur monitoring yang didokumentasikan:

```text
Node Exporter
      ↓
cAdvisor
      ↓
Prometheus
      ↓
Python Backend
      ↓
Flask API
      ↓
Dashboard
      ↓
Telegram Notification
```

SIOD diposisikan sebagai operational monitoring layer yang memanfaatkan data dari monitoring stack tersebut.

Project tidak ditujukan untuk menggantikan Prometheus atau Grafana, tetapi memberikan layer operasional yang lebih sederhana untuk membaca kondisi infrastructure dan menangani incident.

---

## 6. Validasi Sistem

Beberapa komponen dilakukan pengecekan secara langsung:

| Komponen                   | Status       |
| -------------------------- | ------------ |
| Backend                    | Checked      |
| Telemetry API              | Checked      |
| Incident Manager           | Refined      |
| Incident Logging           | Refined      |
| Telegram Notification      | Tested       |
| Dashboard HTML             | Updated      |
| Dashboard CSS              | Redesigned   |
| README                     | Updated      |
| Architecture Documentation | Consolidated |

---

## 7. Kendala yang Ditemukan

Beberapa kendala yang ditemukan selama proses refinement:

### 7.1. Potensi Duplicate Logging

Terdapat komponen lama yang masih memiliki mekanisme analyzer/logging tersendiri.

Hal ini berpotensi menyebabkan:

* duplicate incident processing
* duplicate notification
* log yang tidak konsisten

Solusinya adalah melakukan audit terhadap alur incident dan menentukan komponen yang menjadi sumber utama pengelolaan incident.

---

### 7.2. Incident Recovery

Lifecycle incident tidak hanya membutuhkan pencatatan ketika threshold terlampaui, tetapi juga membutuhkan event ketika kondisi kembali normal.

Karena itu recovery perlu diperlakukan sebagai bagian dari lifecycle incident, bukan hanya sebagai perubahan metric.

---

### 7.3. Konsistensi UI

Setelah redesign CSS, tampilan dashboard perlu diuji secara visual karena perubahan pada satu komponen dapat memengaruhi layout komponen lainnya.

Testing dilakukan secara iteratif dengan melihat hasil aktual dashboard dan kemudian melakukan adjustment terhadap CSS.

---

## 8. Hasil Akhir Hari Ini

Pada akhir sesi pengembangan:

* Backend SIOD telah diaudit.
* Incident management telah diperiksa dan diperbaiki.
* Logging incident telah dirapikan.
* Telegram notification berhasil diverifikasi.
* Telemetry API berhasil divalidasi.
* Dashboard HTML diperbarui.
* CSS dashboard dirombak.
* Dokumentasi arsitektur diperjelas.
* README diperbarui.
* Project masuk ke tahap persiapan dokumentasi video.

Secara keseluruhan, pekerjaan hari ini merupakan tahap **refinement dan stabilization** sebelum masuk ke tahap dokumentasi dan finalisasi project.

---

## 9. Next Step

Rencana pekerjaan berikutnya:

1. Melakukan final verification seluruh monitoring flow.
2. Memastikan incident lifecycle berjalan konsisten.
3. Memastikan tidak terdapat duplicate Telegram notification.
4. Melakukan final UI testing.
5. Melakukan cleanup file yang sudah tidak digunakan.
6. Finalisasi README.
7. Mempersiapkan video dokumentasi SIOD.
8. Menyiapkan repository untuk final presentation/demo.

---

## 10. Tracking

```text
[SIOD-2026-08-27]

Phase:
Development & Refinement

Focus:
Backend
Incident Management
Logging
Telegram
Telemetry
Dashboard UI
Documentation

Status:
REFINEMENT COMPLETED

Next:
Final Verification → Documentation → Demo
```

---

**Report Date:** 27 August 2026
**Project:** SIOD — Smart Infrastructure Operations Dashboard
