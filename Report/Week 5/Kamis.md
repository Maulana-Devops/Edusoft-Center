# 🚀 Sprint 2 Report: Core Observability Engine & Interactive Dashboard

**Project:** Smart Monitor / GrogolSIOD  
**Date Completed:** 20 August 2026  
**Status:** Completed (100%)  

---

## 📌 Executive Summary

Pada Sprint 2, pengembangan berfokus pada penyempurnaan engine pengumpul metrik, stabilitas API backend, visualisasi data real-time pada dashboard web, serta otomatisasi layanan server berbasis `systemd`. Seluruh sistem kini beroperasi penuh 24/7 di latar belakang dengan sinkronisasi zona waktu lokal (WIB).

---

## 🛠️ Key Achievements & Implementation

### 1. Collector Engine & State Tracking (`collector.py` & `main.py`)
* **Resource Monitoring:** Pengumpulan data penggunaan CPU (%), RAM (MiB/%), dan jumlah kontainer Docker secara real-time.
* **Event State Tracking:** Deteksi otomatis perubahan status kontainer (`CONTAINER_UP` dan `CONTAINER_DOWN`).
* **Forensic Anomaly Logging:** Pencatatan log insiden dan lonjakan beban (*CPU Spike*) ke file JSON terstruktur (`incident_log.json`).

### 2. Backend API & System Service (`api.py`)
* **Endpoint Optimization:** Penataan ulang route `/api/status` dan `/api/incidents` untuk menyajikan data terenkapsulasi secara aman.
* **CORS Integration:** Implementasi `Flask-CORS` untuk fleksibilitas akses dashboard dari berbagai *device* dalam jaringan lokal.
* **Timezone Synchronization:** Pengaturan sistem OS dan log ke zona waktu **Asia/Jakarta (WIB)**.
* **Systemd Daemon Automation:**
  * Created `smart-monitor.service` (Engine Monitoring Service).
  * Created `smart-api.service` (Flask API Service).

### 3. Frontend & UI Redesign (`dashboard.html`)
* **Interactive Visualizations (Chart.js):**
  * **Line Chart:** Tren pergerakan CPU % dan RAM % secara real-time.
  * **Bar Chart:** Komparasi penggunaan resource CPU vs RAM.
  * **Doughnut Chart:** Distribusi tipe insiden (`ANOMALY`, `CONTAINER_DOWN`, `CONTAINER_UP`).
* **Auto-Polling:** Pembaruan data otomatis setiap 3 detik tanpa butuh *refresh* halaman manual.
* **Responsive Layout:** Tampilan antarmuka modern berbasis Tailwind CSS & FontAwesome.

### 4. Container Remote Control Panel & Real-time Action Triggers
* **Docker Engine SDK Integration:** Pengontrolan kontainer secara langsung melalui web dashboard menggunakan API Docker SDK (`/var/run/docker.sock`).
* **Interactive Control Actions:**
  * **Start:** Menjalankan kontainer yang berstatus `EXITED` langsung dari tabel dashboard.
  * **Restart:** Melakukan pemulihan (*reboot*) cepat pada kontainer yang bermasalah.
  * **Stop / Down:** Menghentikan kontainer yang sedang berjalan (*running*).
* **Accurate Active Container Counting:** Optimasi logika penghitungan kontainer pada kartu statistik *Active Containers* agar hanya memproses kontainer dengan status `RUNNING` (menghapus opsi `all=True` pada pengumpulan metrik ringkasan).

### 5. Dynamic Incident Logging & Precision Telegram Alerts
* **In-Memory & Persistent Forensic Logger:** Integrasi fungsi `log_incident()` dinamis. Setiap aksi interaktif kontainer (*Start*, *Restart*, *Stop*) secara otomatis diinjeksi ke daftar *Forensic Incident Logs & Anomalies* terbaru di sisi teratas tabel.
* **Telegram Bot Integration:** Pengiriman notifikasi darurat secara otomatis ke Telegram Admin saat terjadi insiden atau aksi berkategori `HIGH` Severity.
* **Timestamp Hardening (WIB):** Standarisasi penanganan zona waktu pada payload Telegram dan *event log* menggunakan konversi `astimezone(pytz.timezone('Asia/Jakarta'))` untuk menjamin presisi waktu lokal 100% pas.

### 6. Template Engine & Architecture Bug Fixes
* **Jinja2 Path Resolution:** Penyelesaian masalah `jinja2.exceptions.TemplateNotFound` melalui pemetaan *absolute path* dinamis (`TEMPLATE_DIR` dan `STATIC_DIR`) berbasis `os.path.abspath(__file__)` pada `backend/api.py`.

---

## 🧪 Testing & Verification Results

| Test Scenario | Action Executed | Expected Result | Status |
| :--- | :--- | :--- | :--- |
| **Systemd Service** | `systemctl status smart-monitor smart-api` | Kedua service berstatus `active (running)` | **PASSED** |
| **Container Up Event** | `docker run -d --name test-nginx nginx:alpine` | Count kontainer bertambah, event `CONTAINER_UP` tercatat di log | **PASSED** |
| **Container Down Event** | `docker stop test-nginx` | Status berubah ke `CRITICAL ANOMALIES`, event `CONTAINER_DOWN` tercatat di log | **PASSED** |
| **Timezone Accuracy** | Verifikasi jam log vs UI & Telegram | Jam log forensik dan alert Telegram cocok dengan WIB (Asia/Jakarta) | **PASSED** |
| **Container Control Action** | Klik tombol **Start / Restart / Stop** pada dashboard | Kontainer di server merespons, log insiden bertambah, dan Telegram alert terkirim | **PASSED** |
| **Active Count Precision** | Menghentikan 1 kontainer dari 5 kontainer aktif | Kartu *Active Containers* berkurang menjadi 4, sementara daftar kontainer tetap menampilkan status `EXITED` | **PASSED** |
| **Flask Route Stability** | Menjalankan API dari direktori apa saja (`/root` atau `/backend`) | Halaman `dashboard.html` ter-render sempurna tanpa error Jinja2 | **PASSED** |

---

## 📁 File Structure Updates

```text
smart-monitor/
├── backend/
│   ├── api.py               # Flask REST API, Jinja Path Fix, Docker Control & Telegram Alert
│   ├── collector.py         # Docker & System Metrics Collector
│   └── main.py              # Anomaly Detection & Monitoring Engine
├── frontend/
│   ├── static/              # Dashboard Assets & CSS/JS Libraries
│   └── templates/
│       └── dashboard.html   # Real-time Chart.js & Remote Control Panel
├── logs/
│   ├── current_status.json  # Real-time System Metrics
│   └── incident_log.json    # Persistent Forensic Incident Logs
└── /etc/systemd/system/
    ├── smart-api.service    # API Daemon
    └── smart-monitor.service# Collector Daemon
