Berikut adalah dokumen **`docs/SPRINT-01.md`** lengkap dalam format Markdown standar yang siap kamu salin dan commit ke repositori GitHub proyek PKL milikmu.

---

```markdown
# 🚀 SPRINT-01: Foundation, Core Engine & Telegram Alerting

## 📌 Ringkasan Sprint
- **Periode Execution:** 08 Agustus 2026 – 19 Agustus 2026
- **Target Utama:** Membangun fondasi engine monitoring infrastruktur real-time, kalkulasi *Health Score*, deteksi *CPU Spike* / *RAM Overload*, serta penanganan insiden kontainer Docker dengan notifikasi Telegram otomatis.
- **Status:** ✅ Completed / Verifikasi Berhasil

---

## 🎯 Tujuan & Scope
1. **Real-time Metric Collection:** Mengambil metrik CPU, RAM, dan status kontainer Docker (`cms_vulner`, `db_perpus`, `pma_perpus`) secara periodik.
2. **Health Engine V2:** Menghitung skor kesehatan sistem (*Health Score*) dan status kesehatan (`STABLE`, `DEGRADED`, `CRITICAL`).
3. **Anomaly & Persistent Load Detection:** Menentukan ambang batas lonjakan CPU/RAM serta memicu status **Firing** jika beban berlangsung lama.
4. **DevOps Telegram Notifier:** Mengirimkan notifikasi Telegram otomatis saat kontainer mengalami perubahaan status (*DOWN* / *RECOVERY UP*) dan saat terjadi anomali beban sistem.

---

## 🏗️ Arsitektur Sistem Sprint 1

```text
  ┌─────────────────────────────────────────────────────────┐
  │                    Docker Engine                        │
  │   [ cms_vulner ]      [ db_perpus ]    [ pma_perpus ]   │
  └──────────┬──────────────────┬─────────────────┬─────────┘
             │                  │                 │
             ▼                  ▼                 ▼
  ┌─────────────────────────────────────────────────────────┐
  │                   backend/collector.py                  │
  │             (Fetches System & Docker Metrics)           │
  └─────────────────────────────┬───────────────────────────┘
                                │
                                ▼
  ┌─────────────────────────────────────────────────────────┐
  │                backend/health_engine.py                 │
  │    (Calculates Health Score, Baseline & CPU Spikes)     │
  └─────────────────────────────┬───────────────────────────┘
                                │
                                ▼
  ┌─────────────────────────────────────────────────────────┐
  │                  backend/notifier.py                    │
  │            (Sends Alerts via Telegram API)              │
  └─────────────────────────────┬───────────────────────────┘
                                │
                                ▼
                   📱 Telegram Alert Channel

```

---

## 💻 Hasil Implementasi Kode & Fitur

### 1. Collector & Core Monitoring (`backend/main.py` & `collector.py`)

* Melakukan *polling* statistik sistem setiap 5 detik.
* Melacak *state* kontainer Docker untuk mendeteksi perubahan jumlah kontainer yang aktif (`PREV_CONTAINER_COUNT`).

### 2. Health & Spike Engine (`backend/health_engine.py`)

* **Formula Health Score:** Penilaian dinamis dari skala 0% – 100% berdasarkan persentase pemakaian CPU, RAM, dan ketersediaan kontainer.
* **Counter Multi-Siklus (Firing Logic):** Jika lonjakan CPU bertahan lebih dari 3 siklus berturut-turut ($\ge 15$ detik), sistem menaikkan alert dari `CPU_SPIKE` biasa menjadi **`FIRING_CPU`**.

### 3. Telegram Notifier (`backend/notifier.py`)

Mendukung format pesan *legacy / custom template*:

* **Container Down:** `🚨 ALERT DEVOPS`
* **Container Recovery:** `✅ RESOLVED DEVOPS`
* **CPU Spike:** `SMART MONITOR ALERT: HIGH CPU ANOMALY`
* **Persistent Heavy Load:** `**Firing**` (Prometheus-like Alertmanager Style)

---

## 🧪 Skenario Pengujian & Hasil Verification

| Scenario / Test Case | Perintah Simulasi | Hasil Ekspektasi | Status Verification |
| --- | --- | --- | --- |
| **1. Normal Monitoring** | `python3 backend/main.py` | Log terminal menampilkan CPU, RAM, Container Count, dan Health Score real-time. | PASSED ✅ |
| **2. Container Down** | `docker stop db_perpus` | Notifikasi `🚨 ALERT DEVOPS: Container db_perpus DOWN!` masuk ke Telegram. | PASSED ✅ |
| **3. Container Recovery** | `docker start db_perpus` | Notifikasi `✅ RESOLVED DEVOPS: Container db_perpus UP kembali` masuk ke Telegram. | PASSED ✅ |
| **4. CPU Spike Anomaly** | `docker exec -d cms_vulner timeout 30s sha256sum /dev/zero` | Alert `HIGH CPU ANOMALY` langsung terkirim dalam 5 detik pertama. | PASSED ✅ |
| **5. Persistent Load (Firing)** | Beban CPU dilanjutkan $> 15$ detik | Alert `**Firing**` terkirim karena beban tidak kunjung reda. | PASSED ✅ |

---

## 📦 Deliverables & File Changes

* `backend/main.py` — Engine monitoring utama & penanganan loop per 5 detik.
* `backend/collector.py` — *Integration module* dengan Docker SDK & System API.
* `backend/health_engine.py` — Modul logika skor kesehatan dan batas ambang anomali.
* `backend/notifier.py` — Integration Telegram Bot API untuk pengiriman pesan terformat.
* `backend/incident.py` — Penulisan status terkini dan log kejadian ke `logs/`.

---

## 📝 Kesimpulan & Transition ke Sprint 2

Seluruh fondasi backend v1 dan integrasi Telegram telah siap dan teruji dengan baik. Sistem ini menjadi landasan utama sebelum dilakukannya **Refactoring & Modularization (SIOD Core Foundation)** pada **Sprint 2**.

```

---

### 💡 Cara Menyimpan File Ini di Server
Jalankan perintah ini di terminal server Debian milikmu untuk membuat filenya secara otomatis:

```bash
mkdir -p ~/smart-monitor/docs

cat << 'EOF' > ~/smart-monitor/docs/SPRINT-01.md
# 🚀 SPRINT-01: Foundation, Core Engine & Telegram Alerting

## 📌 Ringkasan Sprint
- **Periode Execution:** 08 Agustus 2026 – 19 Agustus 2026
- **Target Utama:** Membangun fondasi engine monitoring infrastruktur real-time, kalkulasi Health Score, deteksi CPU Spike / RAM Overload, serta penanganan insiden kontainer Docker dengan notifikasi Telegram otomatis.
- **Status:** ✅ Completed / Verifikasi Berhasil

---

## 🎯 Tujuan & Scope
1. **Real-time Metric Collection:** Mengambil metrik CPU, RAM, dan status kontainer Docker (`cms_vulner`, `db_perpus`, `pma_perpus`) secara periodik.
2. **Health Engine V2:** Menghitung skor kesehatan sistem (Health Score) dan status kesehatan (`STABLE`, `DEGRADED`, `CRITICAL`).
3. **Anomaly & Persistent Load Detection:** Menentukan ambang batas lonjakan CPU/RAM serta memicu status **Firing** jika beban berlangsung lama.
4. **DevOps Telegram Notifier:** Mengirimkan notifikasi Telegram otomatis saat kontainer mengalami perubahaan status (*DOWN* / *RECOVERY UP*) dan saat terjadi anomali beban sistem.

---

## 🏗️ Arsitektur Sistem Sprint 1

```text
  ┌─────────────────────────────────────────────────────────┐
  │                    Docker Engine                        │
  │   [ cms_vulner ]      [ db_perpus ]    [ pma_perpus ]   │
  └──────────┬──────────────────┬─────────────────┬─────────┘
             │                  │                 │
             ▼                  ▼                 ▼
  ┌─────────────────────────────────────────────────────────┐
  │                   backend/collector.py                  │
  │             (Fetches System & Docker Metrics)           │
  └─────────────────────────────┬───────────────────────────┘
                                │
                                ▼
  ┌─────────────────────────────────────────────────────────┐
  │                backend/health_engine.py                 │
  │    (Calculates Health Score, Baseline & CPU Spikes)     │
  └─────────────────────────────┬───────────────────────────┘
                                │
                                ▼
  ┌─────────────────────────────────────────────────────────┐
  │                  backend/notifier.py                    │
  │            (Sends Alerts via Telegram API)              │
  └─────────────────────────────┬───────────────────────────┘
                                │
                                ▼
                   📱 Telegram Alert Channel

```

---

## 💻 Hasil Implementasi Kode & Fitur

### 1. Collector & Core Monitoring (`backend/main.py` & `collector.py`)

* Melakukan *polling* statistik sistem setiap 5 detik.
* Melacak *state* kontainer Docker untuk mendeteksi perubahan jumlah kontainer yang aktif (`PREV_CONTAINER_COUNT`).

### 2. Health & Spike Engine (`backend/health_engine.py`)

* **Formula Health Score:** Penilaian dinamis dari skala 0% – 100% berdasarkan persentase pemakaian CPU, RAM, dan ketersediaan kontainer.
* **Counter Multi-Siklus (Firing Logic):** Jika lonjakan CPU bertahan lebih dari 3 siklus berturut-turut (>= 15 detik), sistem menaikkan alert dari `CPU_SPIKE` biasa menjadi **`FIRING_CPU`**.

### 3. Telegram Notifier (`backend/notifier.py`)

Mendukung format pesan *legacy / custom template*:

* **Container Down:** `🚨 ALERT DEVOPS`
* **Container Recovery:** `✅ RESOLVED DEVOPS`
* **CPU Spike:** `SMART MONITOR ALERT: HIGH CPU ANOMALY`
* **Persistent Heavy Load:** `**Firing**` (Prometheus-like Alertmanager Style)

---

## 🧪 Skenario Pengujian & Hasil Verification

| Scenario / Test Case | Perintah Simulasi | Hasil Ekspektasi | Status Verification |
| --- | --- | --- | --- |
| **1. Normal Monitoring** | `python3 backend/main.py` | Log terminal menampilkan CPU, RAM, Container Count, dan Health Score real-time. | PASSED ✅ |
| **2. Container Down** | `docker stop db_perpus` | Notifikasi `🚨 ALERT DEVOPS: Container db_perpus DOWN!` masuk ke Telegram. | PASSED ✅ |
| **3. Container Recovery** | `docker start db_perpus` | Notifikasi `✅ RESOLVED DEVOPS: Container db_perpus UP kembali` masuk ke Telegram. | PASSED ✅ |
| **4. CPU Spike Anomaly** | `docker exec -d cms_vulner timeout 30s sha256sum /dev/zero` | Alert `HIGH CPU ANOMALY` langsung terkirim dalam 5 detik pertama. | PASSED ✅ |
| **5. Persistent Load (Firing)** | Beban CPU dilanjutkan > 15 detik | Alert `**Firing**` terkirim karena beban tidak kunjung reda. | PASSED ✅ |

---

## 📦 Deliverables & File Changes

* `backend/main.py` — Engine monitoring utama & penanganan loop per 5 detik.
* `backend/collector.py` — *Integration module* dengan Docker SDK & System API.
* `backend/health_engine.py` — Modul logika skor kesehatan dan batas ambang anomali.
* `backend/notifier.py` — Integration Telegram Bot API untuk pengiriman pesan terformat.
* `backend/incident.py` — Penulisan status terkini dan log kejadian ke `logs/`.

---

## 📝 Kesimpulan & Transition ke Sprint 2

Seluruh fondasi backend v1 dan integrasi Telegram telah siap dan teruji dengan baik. Sistem ini menjadi landasan utama sebelum dilakukannya **Refactoring & Modularization (SIOD Core Foundation)** pada **Sprint 2**.
EOF

```

Setelah ini, dokumen laporan **Sprint 1** sudah tersimpan rapi dan siap kamu commit ke GitHub!

<FollowUp label="Commit dokumen Sprint 1 ke Git dan lanjut ke eksekusi Day 2" query="Saya sudah menyimpan docs/SPRINT-01.md. Sekarang bantu saya melakukan git commit dan melanjutkan refactoring Day 2."/>

```
