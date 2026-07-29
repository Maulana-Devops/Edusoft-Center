# 🚀 Smart Infrastructure Monitor

> AI-assisted Infrastructure Observability Platform built with Python, Flask, Docker, Prometheus, and cAdvisor.

![Python](https://img.shields.io/badge/Python-3.11-blue)
![Flask](https://img.shields.io/badge/Flask-3.x-black)
![Docker](https://img.shields.io/badge/Docker-Enabled-blue)
![Prometheus](https://img.shields.io/badge/Prometheus-Monitoring-orange)
![Status](https://img.shields.io/badge/Version-v1.0-success)

---

# 📖 Overview

Smart Infrastructure Monitor adalah platform monitoring infrastruktur berbasis web yang dikembangkan untuk memantau kondisi server Docker secara **real-time**. Sistem ini mengumpulkan metrik dari container menggunakan **cAdvisor** dan **Prometheus**, kemudian menganalisis data menggunakan Python sebelum ditampilkan dalam dashboard interaktif.

Project ini dibuat sebagai simulasi sederhana dari konsep **Infrastructure Observability** yang umum digunakan pada lingkungan DevOps modern.

---

# ✨ Features

- 📊 Real-time Infrastructure Dashboard
- 🐳 Docker Container Monitoring
- 📈 CPU & RAM Usage Visualization
- ❤️ System Health Score
- 🚨 Incident Detection Engine
- 📋 Incident History Timeline
- 📡 Prometheus Metrics Collection
- 📨 Telegram Alert Integration
- 📉 Severity Classification
- ⚡ AJAX Auto Refresh

---

# 🛠 Tech Stack

| Component | Technology |
|------------|------------|
| Backend | Python 3 |
| Web Framework | Flask |
| Frontend | HTML, CSS, JavaScript |
| Monitoring | Prometheus |
| Container Metrics | cAdvisor |
| Container Platform | Docker |
| Charts | Chart.js |
| Alert | Telegram Bot API |
| Web Server | Nginx |

---

# 🏗 System Architecture

```
Docker Containers
        │
        ▼
    cAdvisor
        │
        ▼
   Prometheus
        │
        ▼
 Analyzer Engine
        │
        ├────────► Incident Log
        │
        ▼
    Flask API
        │
        ▼
 Web Dashboard
```

---

# 📂 Project Structure

```
smart-monitor/

├── analyzer.py
├── api.py
├── requirements.txt
├── README.md
│
├── templates/
│   └── dashboard.html
│
├── static/
│   ├── style.css
│   └── charts.js
│
├── logs/
│   └── incident_log.json
│
└── docs/
```

---

# 📸 Dashboard Preview

> Tambahkan screenshot dashboard di folder **images/**

```
images/dashboard.png
```

Kemudian tampilkan:

```markdown
![Dashboard](images/dashboard.png)
```

---

# ⚙ Installation

Clone repository

```bash
git clone https://github.com/Maulana-Devops/smart-infrastructure-monitor.git
```

Masuk ke project

```bash
cd smart-infrastructure-monitor
```

Buat Virtual Environment

```bash
python3 -m venv venv
```

Aktifkan Virtual Environment

```bash
source venv/bin/activate
```

Install dependency

```bash
pip install -r requirements.txt
```

Jalankan aplikasi

```bash
python3 api.py
```

---

# 📊 Monitoring Stack

- Docker Engine
- cAdvisor
- Prometheus
- Flask API
- Dashboard
- Telegram Alert

---

# 🎯 Project Goals

Project ini dikembangkan untuk mempelajari implementasi:

- Infrastructure Monitoring
- Observability
- Docker Metrics Collection
- Incident Detection
- Backend Development menggunakan Flask
- Integrasi Monitoring Stack
- DevOps Monitoring Workflow

---

# 🚧 Roadmap

## ✅ Version 1.0

- Infrastructure Dashboard
- Incident Timeline
- Health Score
- Telegram Alert
- Docker Monitoring

## 🔄 Version 1.5

- User Authentication
- Multi Dashboard
- Export Report
- Better UI

## 🚀 Version 2.0

- Multi Host Monitoring
- Agent-based Monitoring
- Historical Database
- REST API

## ☁ Version 3.0

- Kubernetes Support
- Cloud Monitoring
- AI Prediction
- Root Cause Analysis

---

# 👨‍💻 Author

**Maulana Aldi Pradana**

SMK Negeri 2 Surakarta

TJKT Student • DevOps Enthusiast • Infrastructure Monitoring

GitHub:
https://github.com/Maulana-Devops

---

# 📄 License

This project is created for educational and portfolio purposes.
