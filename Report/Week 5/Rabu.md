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
