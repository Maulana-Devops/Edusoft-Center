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
* **Responsive Layout:** Tampilan antarmuka modern berbasi Tailwind CSS & FontAwesome.

---

## 🧪 Testing & Verification Results

| Test Scenario | Action Executed | Expected Result | Status |
| :--- | :--- | :--- | :--- |
| **Systemd Service** | `systemctl status smart-monitor smart-api` | Kedua service berstatus `active (running)` | **PASSED** |
| **Container Up Event** | `docker run -d --name test-nginx nginx:alpine` | Count kontainer bertambah, event `CONTAINER_UP` tercatat di log | **PASSED** |
| **Container Down Event**| `docker stop test-nginx` | Status berubah ke `CRITICAL ANOMALIES`, event `CONTAINER_DOWN` tercatat di log | **PASSED** |
| **Timezone Accuracy** | Verifikasi jam log vs UI | Jam log forensik cocok dengan `Grogol Time` (WIB) | **PASSED** |

---

## 📁 File Structure Updates

```text
smart-monitor/
├── backend/
│   ├── api.py               # Flask REST API + CORS Enabled
│   ├── collector.py         # Docker & System Metrics Collector
│   └── main.py              # Anomaly Detection & Monitoring Engine
├── frontend/
│   └── templates/
│       └── dashboard.html   # Real-time Chart.js Dashboard
├── logs/
│   ├── current_status.json  # Real-time System Metrics
│   └── incident_log.json    # Forensic Incident Logs
└── /etc/systemd/system/
    ├── smart-api.service    # API Daemon
    └── smart-monitor.service# Collector Daemon
