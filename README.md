# 🌱 EDAMAME  
**Edge Device AI Monitoring And Metrics Engine**

EDAMAME is a lightweight, extensible **edge AI observability and monitoring system** designed for Raspberry Pi–class devices and AI accelerators (Hailo, Jetson-class, CPU-only).

It provides **real-time health, performance, and AI pipeline metrics** from edge devices and streams them to a centralized dashboard for monitoring, alerts, and analysis.

---

## Why EDAMAME?

Edge AI deployments often fail silently:
- FPS drops due to thermal throttling
- Pipelines hang after days of uptime
- Models change but nobody knows which version broke things
- Devices overheat, reboot, or lose camera feeds

**EDAMAME makes edge AI observable.**

---

## Features

### System Metrics
- CPU usage
- RAM usage
- Disk usage
- CPU temperature
- Throttling & under-voltage flags
- Uptime & reboot detection

### AI Pipeline Metrics
- Inference FPS
- Inference latency (avg / p95)
- Dropped frames
- Pipeline crash detection
- Last successful inference timestamp
- Model version / hash tracking

### Accelerator Support (Extensible)
- Hailo device temperature & utilization *(where available)*
- Accelerator presence & health checks

### Camera & Input Health
- Camera disconnect detection
- Frame freeze detection
- Resolution & format change detection

### Cloud Integration
- HTTPS-based metric ingestion
- JSON-based schema
- Compatible with AWS serverless backends
- Alert-ready (email / webhook)

---

## Supported & Tested Platforms

EDAMAME has been **tested on real hardware**, not just emulators:

| Device | OS | Accelerator |
|------|---|-------------|
| Raspberry Pi 5 | **Bookworm** | Hailo-8 / Hailo-8L |
| Raspberry Pi Zero 2 W | **Bullseye**, **Bookworm** | CPU-only |
| Radxa Rock 5T | **Ubuntu** | CPU / NPU / LiDAR (SSL) |

---

## Architecture Overview

```text
┌────────────────────┐
│  Edge Device       │
│  (RPi / Rock)      │
│                    │
│  EDAMAME Agent     │
│  - System metrics  │
│  - AI metrics      │
│  - Health checks   │
└─────────┬──────────┘
          │ HTTPS (JSON)
          ▼
┌────────────────────┐
│ Cloud Backend      │
│ - API Gateway      │
│ - Lambda           │
│ - Dynamo DB / S3   │
└─────────┬──────────┘
          ▼
┌────────────────────┐
│ Web Dashboard      │
│ - Live metrics     │
│ - Alerts           │
│ - History          │
└────────────────────┘
