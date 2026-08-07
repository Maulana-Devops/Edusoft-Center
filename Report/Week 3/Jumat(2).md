Siap. Berikut satu file Markdown yang merangkum **Sprint 05–09** berdasarkan progres yang kita kerjakan hari ini. Bisa langsung kamu salin ke GitHub, misalnya sebagai `docs/sprint-05-09.md`.

````md
# SIOD AI Agent — Sprint 05–09 Report

**Project:** Smart Infrastructure Operations Dashboard (SIOD)  
**Module:** SIOD AI Agent  
**Period:** Sprint 05–09  
**Environment:** Debian Linux, Python Virtual Environment, Docker, Prometheus, cAdvisor  
**AI Provider:** Google Gemini  
**Project Type:** AI-Assisted Infrastructure Observability

---

## 1. Overview

Pada Sprint 05–09, pengembangan SIOD AI Agent difokuskan pada pembangunan fondasi monitoring dan integrasi data infrastruktur secara nyata.

Tahapan yang dilakukan meliputi:

- Integrasi AI Provider menggunakan Google Gemini.
- Implementasi memory dan metrics history.
- Pengembangan Monitoring Agent.
- Integrasi Prometheus sebagai sumber metrics.
- Pengambilan host-level metrics.
- Pengambilan container-level metrics melalui cAdvisor.
- Analisis penggunaan CPU dan memory setiap container.
- Integrasi hasil monitoring ke Monitoring Agent.
- Pengujian end-to-end pengumpulan metrics.
- Pengujian AI analysis menggunakan data monitoring aktual.

Tujuan utama sprint ini adalah mengubah SIOD AI Agent dari sistem yang sebelumnya menggunakan data simulasi menjadi sistem yang mulai menggunakan **real infrastructure metrics**.

---

# Sprint 05 — AI Provider Integration

## Tujuan

Menyelesaikan integrasi AI Gateway dengan AI Provider sehingga SIOD AI Agent dapat berkomunikasi dengan model AI eksternal.

## Implementasi

AI Gateway digunakan sebagai abstraction layer antara aplikasi SIOD dan AI Provider.

Konfigurasi provider menggunakan environment variable:

```env
AI_PROVIDER=google
````

Konfigurasi model dan API key dikelola melalui environment variable agar tidak ditulis langsung di source code.

Contoh konfigurasi:

```python
import os
from dotenv import load_dotenv

load_dotenv()

AI_PROVIDER = os.getenv("AI_PROVIDER", "google")

MODEL_NAME = os.getenv(
    "MODEL_NAME",
    "gemini-3.5-flash"
)

GEMINI_API_KEY = os.getenv("GEMINI_API_KEY")
```

## Pengujian

AI Gateway berhasil dijalankan menggunakan:

```bash
python main.py
```

Output menunjukkan bahwa AI Provider telah berhasil terhubung dan memberikan response dari Gemini.

Contoh:

```text
Hello! I’m Gemini, a large language model developed by Google...
```

## Hasil

Sprint 05 berhasil.

AI Gateway sudah dapat:

* Membaca konfigurasi provider.
* Mengambil API key dari environment.
* Menghubungkan aplikasi dengan Google Gemini.
* Mengirim request ke AI model.
* Menerima response dari AI model.

---

# Sprint 06 — Memory & Metrics History

## Tujuan

Membangun mekanisme penyimpanan history metrics agar AI Agent tidak hanya menganalisis kondisi saat ini, tetapi juga memiliki data historis sebagai konteks.

## Struktur Memory

Struktur directory yang digunakan:

```text
memory/
├── history.py
├── incidents/
├── __init__.py
├── manager.py
├── metrics/
│   └── history.json
├── __pycache__/
└── reports/
```

File utama:

```text
memory/metrics/history.json
```

digunakan untuk menyimpan history metrics.

## Contoh Data

History metrics memiliki struktur seperti:

```json
[
    {
        "timestamp": "2026-08-06T22:49:53.811870",
        "metrics": {
            "cpu": "92%",
            "memory": "84%",
            "disk": "55%",
            "containers": 12,
            "health_score": 72
        }
    }
]
```

Data history kemudian dapat digunakan sebagai context tambahan untuk AI Agent.

## Hasil

Memory system berhasil digunakan untuk:

* Menyimpan metrics.
* Membaca metrics sebelumnya.
* Menyediakan historical context.
* Menampilkan perubahan metrics dari waktu ke waktu.

Contoh hasil:

```text
Metrics History

[
    {
        'timestamp': '2026-08-06T22:49:53.811870',
        'metrics': {
            'cpu': '92%',
            'memory': '84%',
            'disk': '55%',
            'containers': 12,
            'health_score': 72
        }
    },
    ...
]
```

---

# Sprint 07 — Monitoring Agent

## Tujuan

Membangun Monitoring Agent sebagai komponen yang bertanggung jawab mengumpulkan metrics dan mengirimkannya ke AI untuk dianalisis.

## Konsep

Alur Monitoring Agent:

```text
Infrastructure
      │
      ▼
Metrics Collector
      │
      ▼
Monitoring Agent
      │
      ├── Current Metrics
      │
      ├── Metrics History
      │
      ▼
Prompt Builder
      │
      ▼
AI Gateway
      │
      ▼
AI Analysis
```

## Monitoring Agent

Monitoring Agent bertugas:

1. Mengambil metrics.
2. Membaca historical metrics.
3. Menyusun context.
4. Membuat prompt.
5. Mengirim prompt ke AI Gateway.
6. Menerima hasil analisis AI.

## Prompt Builder

Dalam proses pengembangan ditemukan masalah ketika template prompt menggunakan JSON secara langsung bersama:

```python
template.format(**kwargs)
```

Karakter `{}` pada JSON dianggap sebagai placeholder oleh Python.

Hal tersebut menyebabkan error:

```text
KeyError: '\n    "status"'
```

Masalah diselesaikan dengan melakukan escaping pada curly braces JSON.

Contoh:

```text
{{
    "status": "...",
    "severity": "..."
}}
```

Dengan demikian `{}` tetap dianggap sebagai karakter biasa dan bukan placeholder Python.

## Hasil AI Analysis

Monitoring Agent berhasil menghasilkan analisis seperti:

```text
Current Status
The infrastructure node is currently operating in a degraded state...

Resource Analysis
CPU (92%): Operating at near-saturation levels.
Memory (84%): High utilization.
Disk (55%): Healthy.

Severity
High

Recommended Actions
1. Identify Resource-Intensive Containers.
2. Analyze Container Logs.
3. Review Resource Limits.
4. Request Additional Data.
```

## Hasil

Sprint 07 berhasil.

Monitoring Agent sudah dapat menggabungkan:

* Current metrics.
* Metrics history.
* Prompt Builder.
* AI Gateway.
* AI analysis.

---

# Sprint 08 — Prometheus Integration

## Tujuan

Mengubah sumber metrics dari data simulasi menjadi data nyata yang diperoleh dari Prometheus.

Sebelumnya metrics masih berupa nilai hardcoded:

```python
return {
    "cpu": "92%",
    "memory": "84%",
    "disk": "55%",
    "containers": 12,
    "health_score": 72
}
```

Pada Sprint 08, metrics mulai diambil secara langsung menggunakan Prometheus HTTP API.

## Prometheus Client

Dibuat client untuk berkomunikasi dengan Prometheus:

```python
import requests


class PrometheusClient:

    def __init__(self, url):
        self.url = url.rstrip("/")

    def query(self, promql):

        endpoint = f"{self.url}/api/v1/query"

        response = requests.get(
            endpoint,
            params={
                "query": promql
            }
        )

        response.raise_for_status()

        return response.json()
```

## Prometheus URL

Konfigurasi ditambahkan ke environment:

```env
PROMETHEUS_URL=http://localhost:9090
```

dan dibaca melalui:

```python
PROMETHEUS_URL = os.getenv(
    "PROMETHEUS_URL",
    "http://localhost:9090"
)
```

## Pengujian Prometheus

Prometheus API berhasil diakses menggunakan:

```bash
curl http://localhost:9090/api/v1/query?query=up
```

Response:

```json
{
    "status": "success",
    "data": {
        "resultType": "vector"
    }
}
```

Hal ini menunjukkan Prometheus API dapat diakses dengan baik.

## Host CPU

Query CPU:

```promql
100 - (
    avg(rate(node_cpu_seconds_total{mode="idle"}[5m]))
    * 100
)
```

Hasil pengujian:

```text
10.6477%
```

## Host Memory

Query memory:

```promql
(
    (
        node_memory_MemTotal_bytes
        -
        node_memory_MemAvailable_bytes
    )
    /
    node_memory_MemTotal_bytes
) * 100
```

Hasil:

```text
51.29%
```

## Container Count

Query:

```promql
count(container_last_seen)
```

Hasil:

```text
8
```

## Hasil Host Metrics

Setelah integrasi Prometheus, Monitoring Agent berhasil menghasilkan metrics aktual:

```python
{
    "cpu": 9.34,
    "memory": 51.4,
    "disk": 0.0,
    "containers": 8,
    "health_score": 81
}
```

Pada pengujian berikutnya kondisi host berubah menjadi:

```python
{
    "cpu": 9.73,
    "memory": 52.68,
    "disk": 0,
    "containers": 7,
    "health_score": 100
}
```

Perubahan nilai tersebut menunjukkan bahwa data yang digunakan sudah berasal dari kondisi infrastructure aktual, bukan lagi nilai simulasi.

---

# Sprint 09 — Container Resource Monitoring

## Tujuan

Mengembangkan monitoring sampai level container sehingga SIOD AI Agent dapat mengetahui container mana yang menggunakan resource paling besar.

Data container diperoleh melalui:

```text
cAdvisor
   │
   ▼
Prometheus
   │
   ▼
PrometheusClient
   │
   ▼
PrometheusMetrics
   │
   ▼
Monitoring Agent
```

---

## cAdvisor Integration

cAdvisor digunakan sebagai sumber metrics container.

Container yang tersedia pada monitoring stack:

```text
prometheus
grafana
node-exporter
cadvisor
```

Sementara container aplikasi lain juga terdeteksi:

```text
cms_vulner
db_perpus
pma_perpus
```

## Container CPU Metrics

Metrics diambil dari:

```promql
container_cpu_usage_seconds_total
```

Hasil kemudian diproses menjadi CPU utilization per container.

Contoh hasil:

```text
--- CPU ---

cadvisor               2.3481%
grafana                1.1151%
node-exporter          0.6346%
prometheus             0.6181%
db_perpus              0.0789%
pma_perpus             0.0093%
cms_vulner             0.0083%
```

Dari hasil tersebut dapat diketahui bahwa:

```text
cadvisor
```

menjadi container dengan penggunaan CPU tertinggi pada saat pengujian.

---

# Container Memory Monitoring

Selain CPU, SIOD AI Agent juga mengambil memory usage setiap container.

Contoh hasil:

```text
--- MEMORY ---

grafana                  416.93 MB
cadvisor                 253.81 MB
db_perpus                213.83 MB
prometheus               167.82 MB
pma_perpus                42.59 MB
cms_vulner                33.53 MB
node-exporter             28.42 MB
```

Berdasarkan hasil tersebut, container dengan penggunaan memory terbesar adalah:

```text
grafana
```

diikuti oleh:

```text
cadvisor
db_perpus
prometheus
```

---

# Monitoring Agent Integration Test

Setelah host metrics dan container metrics berhasil dikumpulkan, dilakukan pengujian Monitoring Agent.

Command:

```bash
python test_monitoring_agent.py
```

Hasil:

```text
========================================
        SIOD MONITORING AGENT
========================================

=== HOST METRICS ===

{
    'cpu': 9.73,
    'memory': 52.68,
    'disk': 0,
    'containers': 7,
    'health_score': 100
}

=== CONTAINER CPU ===

cadvisor               2.6014%
grafana                1.0929%
node-exporter          0.6669%
prometheus             0.5630%
db_perpus              0.0836%
cms_vulner             0.0092%
pma_perpus             0.0092%

=== CONTAINER MEMORY ===

grafana                  416.95 MB
cadvisor                 246.96 MB
db_perpus                213.83 MB
prometheus               168.95 MB
pma_perpus                42.59 MB
cms_vulner                33.53 MB
node-exporter             28.34 MB

========================================
        COLLECTION SUCCESS
========================================
```

Hasil tersebut menunjukkan bahwa collection pipeline telah berjalan dengan baik.

---

# AI Infrastructure Analysis

Setelah metrics aktual berhasil dikumpulkan, data tersebut dikirim ke AI Agent untuk dianalisis.

Contoh hasil analisis:

```text
Current Status

The infrastructure is currently healthy.
The host has a health score of 100, and all resource
utilization metrics are well within safe operating limits.
There are 7 containers running on the host.
```

## Resource Analysis

AI mengidentifikasi:

```text
CPU:
10.29%

Memory:
53.26%

Disk:
0%

Containers:
7
```

AI juga menganalisis resource consumption masing-masing container.

Container dengan penggunaan CPU tertinggi:

```text
cadvisor
```

Container dengan penggunaan memory tertinggi:

```text
grafana
```

## Severity

AI memberikan status:

```text
Green / Healthy
```

karena resource host masih berada pada kondisi aman.

## Recommended Actions

AI memberikan rekomendasi:

1. Continue Standard Monitoring.
2. Establish memory baseline.
3. Monitor Grafana, cAdvisor, dan database.
4. Verify disk reporting.

---

# Technical Architecture After Sprint 09

Setelah Sprint 05–09, arsitektur SIOD AI Agent menjadi:

```text
                    ┌──────────────────┐
                    │   Infrastructure │
                    │     Server       │
                    └────────┬─────────┘
                             │
              ┌──────────────┴──────────────┐
              │                             │
              ▼                             ▼
       Node Exporter                    cAdvisor
              │                             │
              │                             │
              └──────────────┬──────────────┘
                             ▼
                       ┌─────────────┐
                       │ Prometheus  │
                       └──────┬──────┘
                              │
                              ▼
                     Prometheus Client
                              │
                              ▼
                     Prometheus Metrics
                              │
                              ▼
                     Monitoring Agent
                              │
                ┌─────────────┴─────────────┐
                │                           │
                ▼                           ▼
        Current Metrics              Metrics History
                │                           │
                └─────────────┬─────────────┘
                              ▼
                       Prompt Builder
                              │
                              ▼
                         AI Gateway
                              │
                              ▼
                        Google Gemini
                              │
                              ▼
                       AI Analysis
```

---

# Components Implemented

## AI Gateway

Bertanggung jawab sebagai abstraction layer untuk AI provider.

```text
ai_gateway/
├── gateway.py
├── gemini.py
├── provider.py
└── __init__.py
```

## Memory

Bertanggung jawab menyimpan metrics history.

```text
memory/
├── history.py
├── manager.py
├── storage.py
├── metrics/
│   └── history.json
├── incidents/
└── reports/
```

## Prometheus Tools

Digunakan untuk mengambil infrastructure metrics.

```text
tools/
├── prometheus/
│   ├── client.py
│   ├── metrics.py
│   ├── queries.py
│   └── __init__.py
```

## Docker Tools

Disiapkan untuk kebutuhan monitoring container.

```text
tools/
├── docker/
│   ├── client.py
│   └── __init__.py
```

## System Tools

Digunakan sebagai bagian dari infrastructure collection layer.

```text
tools/
└── system/
    ├── collector.py
    └── __init__.py
```

---

# Testing Performed

Beberapa pengujian yang telah dilakukan:

### AI Provider

```bash
python main.py
```

Status:

```text
SUCCESS
```

### Prometheus

```bash
python test_prometheus.py
```

Status:

```text
SUCCESS
```

Host metrics berhasil diperoleh dari Prometheus.

### Container Resource

```bash
python test_container_resources.py
```

Status:

```text
SUCCESS
```

CPU dan memory masing-masing container berhasil diperoleh.

### Monitoring Agent

```bash
python test_monitoring_agent.py
```

Status:

```text
COLLECTION SUCCESS
```

Host dan container metrics berhasil dikumpulkan.

---

# Problems Encountered & Solutions

## 1. AI Provider Tidak Dikenali

Error:

```text
ValueError: Unsupported AI Provider: gemini
```

Penyebab:

Konfigurasi provider masih menggunakan:

```env
AI_PROVIDER=gemini
```

Solusi:

Mengubah menjadi:

```env
AI_PROVIDER=google
```

---

## 2. Missing python-dotenv

Error:

```text
ModuleNotFoundError: No module named 'dotenv'
```

Solusi:

Mengaktifkan virtual environment dan memastikan dependency tersedia.

```bash
source venv/bin/activate
```

Kemudian dependency `python-dotenv` digunakan untuk membaca `.env`.

---

## 3. MemoryManager Tidak Ditemukan

Error:

```text
ModuleNotFoundError:
No module named 'memory.manager'
```

Penyebab:

Module `memory.manager` belum tersedia pada struktur project saat pemanggilan dilakukan.

Solusi:

Melengkapi struktur memory module dan implementasinya.

---

## 4. Prompt Builder KeyError

Error:

```text
KeyError: '\n    "status"'
```

Penyebab:

JSON object pada prompt menggunakan `{}` yang diproses oleh:

```python
template.format(**kwargs)
```

Solusi:

Melakukan escaping curly braces:

```text
{{
    "status": "..."
}}
```

---

## 5. PrometheusMetrics Abstract Class Error

Error:

```text
TypeError:
Can't instantiate abstract class PrometheusMetrics
with abstract method collect
```

Penyebab:

Class `PrometheusMetrics` mewarisi `BaseTool`, tetapi method abstract `collect()` belum diimplementasikan dengan benar.

Solusi:

Mengimplementasikan method:

```python
def collect(self):
    ...
```

sesuai interface `BaseTool`.

---

## 6. Container Metrics Tidak Ditemukan

Awalnya:

```text
=== CONTAINER RESOURCE ANALYZER ===

No container metrics found.
```

Penyebab:

Query metrics container belum sesuai dengan metrics yang tersedia dari cAdvisor.

Setelah melakukan pemeriksaan terhadap Prometheus, ditemukan metrics:

```text
container_cpu_usage_seconds_total
```

beserta label:

```text
name
image
instance
job
```

Query kemudian disesuaikan agar dapat mengambil data container berdasarkan label `name`.

Hasil akhirnya:

```text
CPU:
cadvisor
grafana
node-exporter
prometheus
db_perpus
pma_perpus
cms_vulner

MEMORY:
grafana
cadvisor
db_perpus
prometheus
pma_perpus
cms_vulner
node-exporter
```

---

# Current System Capability

Setelah menyelesaikan Sprint 05–09, SIOD AI Agent telah memiliki kemampuan:

* [x] AI Provider Integration
* [x] Google Gemini Integration
* [x] AI Gateway
* [x] Memory Manager
* [x] Metrics History
* [x] Monitoring Agent
* [x] Prompt Builder
* [x] Prometheus Client
* [x] Host CPU Monitoring
* [x] Host Memory Monitoring
* [x] Host Disk Monitoring
* [x] Container Count Monitoring
* [x] Container CPU Monitoring
* [x] Container Memory Monitoring
* [x] cAdvisor Integration
* [x] AI Infrastructure Analysis
* [x] Severity Classification
* [x] Infrastructure Recommendations

---

# Final Result

Sprint 05–09 berhasil membawa SIOD AI Agent dari tahap AI integration dan simulated monitoring menuju sistem yang sudah dapat melakukan **real infrastructure monitoring**.

Sistem sekarang memiliki pipeline:

```text
Real Infrastructure
        ↓
Node Exporter / cAdvisor
        ↓
Prometheus
        ↓
Prometheus Client
        ↓
Monitoring Agent
        ↓
Metrics History
        ↓
Prompt Builder
        ↓
AI Gateway
        ↓
Google Gemini
        ↓
Infrastructure Analysis
```

Dengan pipeline tersebut, SIOD AI Agent sudah dapat:

> **Mengambil kondisi infrastructure secara aktual, mengidentifikasi penggunaan resource host dan container, menyimpan historical metrics, kemudian menggunakan AI untuk memberikan analisis kondisi infrastructure dan rekomendasi tindakan.**

---

# Conclusion

Sprint 05–09 telah menyelesaikan fondasi utama dari SIOD AI Agent.

Fokus pengembangan berikutnya dapat diarahkan pada peningkatan kemampuan **analysis dan decision support**, sehingga AI tidak hanya membaca metrics dan memberikan deskripsi, tetapi juga mampu melakukan korelasi antar-metrics, mendeteksi anomaly, menentukan root cause yang lebih terarah, serta menghasilkan rekomendasi berdasarkan kondisi infrastructure secara lebih sistematis.

```
```
