<div align="center">

```
╔═══════════════════════════════════════════════════════════════════════╗
║                                                                       ║
║    ██████╗ ██████╗ ███████╗ ██████╗ ██████╗ ██████╗ ███████╗        ║
║   ██╔═══██╗██╔══██╗██╔════╝██╔════╝██╔═══██╗██╔══██╗██╔════╝        ║
║   ██║   ██║██████╔╝███████╗██║     ██║   ██║██████╔╝█████╗          ║
║   ██║   ██║██╔═══╝ ╚════██║██║     ██║   ██║██╔══██╗██╔══╝          ║
║   ╚██████╔╝██║     ███████║╚██████╗╚██████╔╝██║  ██║███████╗        ║
║    ╚═════╝ ╚═╝     ╚══════╝ ╚═════╝ ╚═════╝ ╚═╝  ╚═╝╚══════╝        ║
║                                                                       ║
║          O B S E R V A B I L I T Y   I N T E L L I G E N C E        ║
║                                                                       ║
╚═══════════════════════════════════════════════════════════════════════╝
```

**Production-Grade HA Observability Platform for Microservices**

*Dynatrace-style Operations · Grafana-style Dashboards · New Relic-style Presentation*

---

![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-3.x-000000?style=for-the-badge&logo=flask&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-8.x-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-3.x-003B57?style=for-the-badge&logo=sqlite&logoColor=white)
![Chart.js](https://img.shields.io/badge/Chart.js-4.x-FF6384?style=for-the-badge&logo=chartdotjs&logoColor=white)
![Jinja2](https://img.shields.io/badge/Jinja2-3.x-B41717?style=for-the-badge&logo=jinja&logoColor=white)

![License](https://img.shields.io/badge/License-MIT-06D6A0?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active_Development-4F6EFF?style=for-the-badge)
![Pages](https://img.shields.io/badge/Pages-20+-FFD166?style=for-the-badge)
![APIs](https://img.shields.io/badge/APIs-40+-FF6B6B?style=for-the-badge)

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Platform Maturity](#-platform-maturity)
- [Tech Stack](#-tech-stack)
- [System Architecture](#-system-architecture)
- [Log & Data Flow](#-log--data-flow)
- [Monitoring Flow](#-monitoring-flow)
- [Module Architecture](#-module-architecture)
- [Backend Structure](#-backend-structure)
- [Database Schema](#-database-schema)
- [API Reference](#-api-reference)
- [Frontend Pages](#-frontend-pages)
- [Feature Highlights](#-feature-highlights)
- [Performance Strategy](#-performance-strategy)
- [Security & RBAC](#-security--rbac)
- [Quick Start](#-quick-start)
- [Roadmap](#-roadmap)

---

## 🔭 Overview

OpsCore is a **production-grade High-Availability observability platform** purpose-built for microservice environments. It combines:

| Dimension | Inspiration | What OpsCore delivers |
|-----------|-------------|----------------------|
| **Operations UX** | Dynatrace | Service-first NOC portal, topology awareness, HA health panels |
| **Dashboarding** | Grafana | Rich chart-driven trend analysis, filter-driven screens |
| **Observability** | New Relic | End-to-end log→analytic→alert pipeline with service scoping |

> The platform is **not starting from zero**. Every module is evolved from a working production codebase — preserving ingestion, analytics, alerting, and UI assets while completing the service-first migration.

---

## 📊 Platform Maturity

```
┌─────────────────────────────────────────────────────────────────────┐
│                        MATURITY MATRIX                              │
├──────────────────────┬────────────────────────┬────────────────────┤
│  ✅  STRONG           │  🔄  PARTIAL            │  🗺️  ROADMAP        │
├──────────────────────┼────────────────────────┼────────────────────┤
│  Log ingestion       │  Service-first model   │  Distributed trace │
│  Analytics engine    │  Microservice deploy   │  Topology view     │
│  Operational dashbd  │  HA platform semantics │  SLO / SLA model   │
│  RBAC + permissions  │  Advanced aggregation  │  Anomaly detection │
│  DB portability      │  Modular backend       │  Alert correlation │
│  Alert rules         │  Near-realtime UX      │  Cluster health    │
│  Audit trail         │  Page-level perf       │  Long-term storage │
│  Service registry    │                        │  Trace / span model│
│  Config management   │                        │                    │
└──────────────────────┴────────────────────────┴────────────────────┘
```

---

## 🛠 Tech Stack

```
┌─────────────────────────────────────────────────────────────────────┐
│                         TECH STACK                                  │
│                                                                     │
│  RUNTIME & FRAMEWORK          STORAGE                               │
│  ┌─────────────────┐          ┌──────────┐  ┌──────────┐           │
│  │  Python 3.11+   │          │  MySQL   │  │  SQLite  │           │
│  │  Flask 3.x      │          │  8.x     │  │  (dev)   │           │
│  │  Jinja2         │          └──────────┘  └──────────┘           │
│  │  Werkzeug       │                                                │
│  └─────────────────┘          TRANSPORT                             │
│                               ┌──────────────────────────┐         │
│  FRONTEND                     │  Paramiko (SSH)           │         │
│  ┌─────────────────┐          │  inotify (local watch)   │         │
│  │  Chart.js 4.x   │          │  SMTP / Webhooks          │         │
│  │  Vanilla JS     │          │  SSE (live streaming)     │         │
│  │  HTML5 / CSS3   │          └──────────────────────────┘         │
│  └─────────────────┘                                                │
│                               BACKGROUND                            │
│  RESILIENCE                   ┌──────────────────────────┐         │
│  ┌─────────────────┐          │  APScheduler             │         │
│  │  Circuit Breaker│          │  Async import queue      │         │
│  │  Retry + backoff│          │  Aggregate rebuild jobs  │         │
│  │  Rate limiting  │          └──────────────────────────┘         │
│  │  Health checks  │                                                │
│  └─────────────────┘                                                │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 🏗 System Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        OPSCORE PLATFORM ARCHITECTURE                        │
└─────────────────────────────────────────────────────────────────────────────┘

  ┌──────────────────────────────────────────────────────────────────────────┐
  │                         CONFIGURATION LAYER                              │
  │                                                                          │
  │   ┌──────────────┐    ┌──────────────────┐    ┌──────────────────────┐  │
  │   │   Config UI  │    │  Service Registry │    │    Host Registry     │  │
  │   │  /config     │    │  core/service_    │    │    hosts table       │  │
  │   │              │    │  registry.py      │    │                      │  │
  │   └──────┬───────┘    └────────┬─────────┘    └──────────┬───────────┘  │
  └──────────┼─────────────────────┼───────────────────────  ┼──────────────┘
             │                     │                          │
             └──────────────────── ▼ ─────────────────────────┘
                          Deployment Mapping
                       (service → host → log_path)
                                   │
             ┌─────────────────────▼──────────────────────────┐
             │               COLLECTOR LAYER                   │
             │                                                  │
             │   ┌───────────────────┐  ┌─────────────────┐   │
             │   │   SSH Importer    │  │  Local Watcher  │   │
             │   │ core/ssh_importer │  │ core/log_watcher│   │
             │   │                   │  │                 │   │
             │   │ • async queue     │  │ • inotify tail  │   │
             │   │ • batch import    │  │ • real-time     │   │
             │   │ • job tracking    │  │ • analytics     │   │
             │   └────────┬──────────┘  └────────┬────────┘   │
             │            │                       │            │
             │   ┌────────▼──────────────────────▼────────┐   │
             │   │          Infra Metrics Collector        │   │
             │   │         core/infra_metrics.py           │   │
             │   │  CPU · Memory · Disk · Load Average     │   │
             │   └─────────────────────────────────────────┘   │
             └──────────────────────┬─────────────────────────┘
                                    │
             ┌──────────────────────▼─────────────────────────┐
             │                 STORAGE LAYER                   │
             │                                                  │
             │   ┌──────────────┐  ┌──────────────────────┐   │
             │   │  logs table  │  │  infra_metrics_latest │   │
             │   │  + service_id│  │  + mysql_monitor_hist │   │
             │   └──────┬───────┘  └──────────────────────┘   │
             │          │                                       │
             │   ┌──────▼───────────────────────────────────┐ │
             │   │         log_analytics  (parsed facts)    │ │
             │   │   endpoint · method · status · latency   │ │
             │   │   ip · user_agent · service_id · ts      │ │
             │   └──────┬───────────────────────────────────┘ │
             │          │                                       │
             │   ┌──────▼───────────────────────────────────┐ │
             │   │       analytics_summary  (aggregates)    │ │
             │   │   service_id · hour_bucket · req_count   │ │
             │   │   p95_latency · error_count · tps        │ │
             │   └──────────────────────────────────────────┘ │
             └──────────────────────┬─────────────────────────┘
                                    │
             ┌──────────────────────▼─────────────────────────┐
             │              PROCESSING LAYER                   │
             │                                                  │
             │  ┌──────────────┐ ┌────────────┐ ┌──────────┐  │
             │  │  Log Parser  │ │ RCA Engine │ │  Alert   │  │
             │  │ core/log_    │ │ core/rca_  │ │  Rules   │  │
             │  │ parser.py    │ │ engine.py  │ │ evaluator│  │
             │  └──────┬───────┘ └─────┬──────┘ └────┬─────┘  │
             │         │               │              │         │
             │  ┌──────▼───────────────▼──────────────▼──────┐ │
             │  │          APScheduler Background Jobs        │ │
             │  │  hourly aggregates · imports · cleanups     │ │
             │  └─────────────────────────────────────────────┘ │
             └──────────────────────┬─────────────────────────┘
                                    │
             ┌──────────────────────▼─────────────────────────┐
             │             PRESENTATION LAYER                  │
             │                                                  │
             │  ┌──────────┐ ┌──────────┐ ┌──────────────┐   │
             │  │  Master  │ │  Trend   │ │    Infra     │   │
             │  │  Portal  │ │ Analysis │ │  Dashboard   │   │
             │  │  /master │ │/analytics│ │   /infra     │   │
             │  └──────────┘ └──────────┘ └──────────────┘   │
             │                                                  │
             │  ┌──────────┐ ┌──────────┐ ┌──────────────┐   │
             │  │  Alerts  │ │   RCA    │ │    Logs /    │   │
             │  │  /alerts │ │  /rca    │ │  Live Logs   │   │
             │  └──────────┘ └──────────┘ └──────────────┘   │
             └─────────────────────────────────────────────────┘
```

---

## 🔄 Log & Data Flow

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         LOG INGESTION PIPELINE                              │
└─────────────────────────────────────────────────────────────────────────────┘

  Configured Host
  (hostname + credentials + log_path + service_id)
         │
         ├─────────────────────────────────────┐
         │                                     │
         ▼                                     ▼
  ┌─────────────────────┐           ┌─────────────────────┐
  │    SSH Importer     │           │   Local Log Watcher │
  │                     │           │                     │
  │  1. connect via SSH │           │  1. inotify MODIFY  │
  │  2. tail log file   │           │  2. read new lines  │
  │  3. batch to queue  │           │  3. direct parse    │
  │  4. job_id tracking │           │                     │
  └──────────┬──────────┘           └──────────┬──────────┘
             │                                  │
             └──────────────┬───────────────────┘
                            │
                            ▼
              ┌─────────────────────────────┐
              │      Log Parser             │
              │  core/log_parser.py         │
              │                             │
              │  regex extract:             │
              │  • timestamp                │
              │  • HTTP method + path       │
              │  • status code              │
              │  • response time (ms)       │
              │  • client IP                │
              │  • user agent               │
              │  • error / exception        │
              └──────────────┬──────────────┘
                             │
              ┌──────────────▼──────────────┐
              │       logs  table           │
              │                             │
              │  id · service_id · host_id  │
              │  timestamp · level          │
              │  raw_message · parsed_json  │
              └──────────────┬──────────────┘
                             │
              ┌──────────────▼──────────────┐
              │    log_analytics  table     │
              │                             │
              │  service_id  ◄── KEY        │
              │  endpoint · method          │
              │  status_code                │
              │  latency_ms                 │
              │  client_ip                  │
              │  is_error · is_probe        │
              │  ts                         │
              └──────────────┬──────────────┘
                             │
              ┌──────────────▼──────────────┐
              │   analytics_summary table   │
              │   (hourly aggregate job)    │
              │                             │
              │  service_id · hour_bucket   │
              │  req_count · error_count    │
              │  p50 · p95 · p99 latency    │
              │  tps_avg · tps_peak         │
              └──────────────┬──────────────┘
                             │
         ┌───────────────────┼──────────────────────┐
         │                   │                       │
         ▼                   ▼                       ▼
  ┌─────────────┐   ┌─────────────────┐   ┌────────────────┐
  │   Trend     │   │ Alerts Engine   │   │  Master Portal │
  │  Analysis   │   │                 │   │  NOC Snapshot  │
  │  /analytics │   │ threshold eval  │   │  /master       │
  │             │   │ notify: SMTP    │   │                │
  └─────────────┘   │         webhook │   └────────────────┘
                    └─────────────────┘
```

---

## 🖥 Monitoring Flow

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      INFRASTRUCTURE MONITORING FLOW                         │
└─────────────────────────────────────────────────────────────────────────────┘

  ┌───────────────────────────────────────────────────────────┐
  │                      Host Config                          │
  │    hostname · ssh_user · ssh_port · credentials           │
  └────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
  ┌───────────────────────────────────────────────────────────┐
  │              Infra Metrics Collector                      │
  │              core/infra_metrics.py                        │
  │                                                           │
  │   SSH connect → run system commands → parse output        │
  │                                                           │
  │   ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌──────────┐  │
  │   │   CPU   │  │ Memory  │  │  Disk   │  │   Load   │  │
  │   │   top   │  │  free   │  │   df    │  │  uptime  │  │
  │   └────┬────┘  └────┬────┘  └────┬────┘  └────┬─────┘  │
  │        └────────────┴────────────┴─────────────┘        │
  └────────────────────────────┬──────────────────────────────┘
                               │
               ┌───────────────┼────────────────────┐
               │               │                    │
               ▼               ▼                    ▼
  ┌────────────────┐  ┌─────────────────┐  ┌──────────────────┐
  │infra_metrics_  │  │mysql_monitor_   │  │mysql_monitor_    │
  │latest          │  │latest           │  │history           │
  │                │  │                 │  │                  │
  │ host_id        │  │ query stats     │  │ time series      │
  │ cpu_pct        │  │ slow queries    │  │ trending         │
  │ mem_pct        │  │ conn count      │  │                  │
  │ disk_pct       │  │ replication lag │  │                  │
  │ load_avg       │  │                 │  │                  │
  │ ts             │  │                 │  │                  │
  └───────┬────────┘  └────────┬────────┘  └────────┬─────────┘
          │                    │                     │
          └────────────────────┼─────────────────────┘
                               │
               ┌───────────────┼───────────────┐
               │               │               │
               ▼               ▼               ▼
  ┌────────────────┐  ┌──────────────┐  ┌───────────────┐
  │  Infra Page    │  │ Master Portal│  │  Alert Engine │
  │  /infra        │  │ /master      │  │               │
  │                │  │              │  │ cpu > 90%     │
  │ host cards     │  │ host health  │  │ mem > 85%     │
  │ CPU/mem/disk   │  │ summary row  │  │ disk > 95%    │
  │ trend charts   │  │ NOC view     │  │ → notify      │
  └────────────────┘  └──────────────┘  └───────────────┘
```

---

## 🧩 Module Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        7 PLATFORM MODULES                                   │
└─────────────────────────────────────────────────────────────────────────────┘

  ┌─────────────────────────────────────────────────────────────────────────┐
  │  MODULE 01 · SERVICE REGISTRY                              [✅ LIVE]    │
  ├─────────────────────────────────────────────────────────────────────────┤
  │  core/service_registry.py  ·  services table  ·  service_deployments   │
  │                                                                         │
  │  Service ──► Deployment ──► Host + log_path                            │
  │     │                                                                   │
  │     ├── name · type · owner_team · sla_tier                            │
  │     ├── multiple deployments per service                               │
  │     └── environment-aware (prod / staging / dev)                       │
  └─────────────────────────────────────────────────────────────────────────┘

  ┌─────────────────────────────────────────────────────────────────────────┐
  │  MODULE 02 · HOST & INFRA MONITORING                       [✅ LIVE]    │
  ├─────────────────────────────────────────────────────────────────────────┤
  │  core/infra_metrics.py  ·  core/mysql_monitor.py                       │
  │                                                                         │
  │  Host ──► SSH Collector ──► infra_metrics_latest ──► Infra Page        │
  │                          └► mysql_monitor_latest ──► DB Monitor        │
  └─────────────────────────────────────────────────────────────────────────┘

  ┌─────────────────────────────────────────────────────────────────────────┐
  │  MODULE 03 · LOGS PLATFORM                                 [✅ LIVE]    │
  ├─────────────────────────────────────────────────────────────────────────┤
  │  core/ssh_importer.py  ·  core/log_watcher.py  ·  core/log_parser.py  │
  │                                                                         │
  │  Ingestion ──► Raw Storage ──► Service-scoped Query ──► Live SSE       │
  │                                                     └──► Export CSV    │
  └─────────────────────────────────────────────────────────────────────────┘

  ┌─────────────────────────────────────────────────────────────────────────┐
  │  MODULE 04 · ANALYTICS ENGINE                           [🔄 EXTENDING] │
  ├─────────────────────────────────────────────────────────────────────────┤
  │  core/log_analytics.py  ·  core/tps_engine.py                          │
  │                                                                         │
  │  log_analytics ──► Aggregate Jobs ──► analytics_summary                │
  │                                   └──► service_hourly_summary (WIP)   │
  │                                   └──► service_endpoint_hourly (WIP)  │
  └─────────────────────────────────────────────────────────────────────────┘

  ┌─────────────────────────────────────────────────────────────────────────┐
  │  MODULE 05 · DASHBOARDS & TREND ANALYSIS                [🔄 EXTENDING] │
  ├─────────────────────────────────────────────────────────────────────────┤
  │  templates/analytics.html  ·  templates/master_portal.html             │
  │                                                                         │
  │  Master Portal (NOC) ──► Service Cards ──► Drill-down                  │
  │  Trend Analysis      ──► Lazy tab load ──► Chart.js renders            │
  │  Infra Dashboard     ──► Host health panels                             │
  └─────────────────────────────────────────────────────────────────────────┘

  ┌─────────────────────────────────────────────────────────────────────────┐
  │  MODULE 06 · ALERTS & RCA                               [🔄 EXTENDING] │
  ├─────────────────────────────────────────────────────────────────────────┤
  │  core/rca_engine.py  ·  core/notifications.py  ·  core/smtp_mailer.py  │
  │                                                                         │
  │  Alert Rule ──► Threshold Eval ──► SMTP / Webhook                      │
  │  RCA Engine ──► Correlate signals ──► Hint generation                  │
  │               (errors + latency + infra health)                        │
  └─────────────────────────────────────────────────────────────────────────┘

  ┌─────────────────────────────────────────────────────────────────────────┐
  │  MODULE 07 · SECURITY & AUDIT                              [✅ LIVE]    │
  ├─────────────────────────────────────────────────────────────────────────┤
  │  core/rbac.py  ·  core/resilience.py  ·  audit_log table               │
  │                                                                         │
  │  Login ──► Role Check ──► Permission Matrix ──► Route Access           │
  │         └──────────────────────────────────► Audit Log entry           │
  └─────────────────────────────────────────────────────────────────────────┘
```

---

## 📁 Backend Structure

```
opscore/
│
├── app.py                          # Flask app · route registry · auth lifecycle
│
├── routes/
│   ├── portal_routes.py            # Master portal + NOC snapshot routes
│   ├── runtime_routes.py           # Service/module dynamic pages
│   ├── analytics_routes.py         # Trend analysis API group
│   ├── config_routes.py            # Config + registry APIs
│   └── (remaining app.py groups)   # Pending extraction
│
├── core/
│   ├── db.py                       # Schema · migrations · CRUD · all analytics queries
│   ├── db_backend.py               # MySQL / SQLite abstraction layer
│   ├── db_bootstrap.py             # MySQL bootstrap + first-run setup
│   │
│   ├── log_analytics.py            # Log-to-analytics parser + enrichment
│   ├── log_parser.py               # Generic log parsing utilities
│   ├── log_watcher.py              # Local log tailer + real-time ingest
│   ├── ssh_importer.py             # Remote log ingestion over SSH
│   ├── tps_engine.py               # TPS calculation + time-series engine
│   │
│   ├── infra_metrics.py            # Host metrics over SSH (CPU/mem/disk)
│   ├── mysql_monitor.py            # Query-based DB health monitor
│   ├── master_portal.py            # NOC aggregation snapshot builder
│   │
│   ├── rca_engine.py               # Rule-based RCA hint generator
│   ├── notifications.py            # Email + webhook dispatch
│   ├── smtp_mailer.py              # SMTP delivery + keyword triggers
│   │
│   ├── resilience.py               # Circuit breakers · retries · rate limiting
│   ├── scheduler.py                # APScheduler background job registry
│   ├── rbac.py                     # Role + permission model
│   └── service_registry.py         # Service-first registry + deployment helpers
│
├── templates/
│   ├── base.html                   # Navigation · service search · layout shell
│   ├── master_portal.html          # NOC / operations overview
│   ├── analytics.html              # Trend analysis dashboard
│   ├── logs.html                   # Log viewer
│   ├── live_logs.html              # Real-time SSE log stream
│   ├── infra.html                  # Infrastructure dashboard
│   ├── alerts.html                 # Alert management
│   ├── rca.html                    # Root cause analysis
│   ├── config.html                 # Platform configuration
│   ├── admin.html                  # Admin centre
│   ├── audit.html                  # Audit trail
│   ├── db_monitor.html             # Database observability
│   ├── incidents.html              # Incident management
│   ├── rfc.html                    # RFC tracker
│   ├── module_dynamic.html         # Service / module detail page
│   └── ...                         # billing · ngw · sap · team · timesheet
│
└── static/
    ├── css/
    └── js/
```

---

## 🗄 Database Schema

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                          CORE DATA MODEL                                    │
│                    service_id threads through every table                   │
└─────────────────────────────────────────────────────────────────────────────┘

  ┌─────────────────┐       ┌──────────────────────────┐
  │    services     │       │    service_deployments   │
  ├─────────────────┤       ├──────────────────────────┤
  │ id (PK)         │──┐    │ id (PK)                  │
  │ name            │  └───►│ service_id (FK)          │
  │ type            │       │ host_id    (FK) ─────────┼──┐
  │ owner_team      │       │ log_path                 │  │
  │ sla_tier        │       │ active                   │  │
  │ created_at      │       └──────────────────────────┘  │
  └─────────────────┘                                      │
                             ┌──────────────────────────┐  │
                             │         hosts            │◄─┘
                             ├──────────────────────────┤
                             │ id (PK)                  │
                             │ hostname                 │
                             │ ip_address               │
                             │ ssh_user                 │
                             │ ssh_port                 │
                             │ environment              │
                             └──────────────────────────┘

  ┌──────────────────────────────────────────────────────────────────────┐
  │                        OBSERVABILITY TABLES                          │
  ├──────────────────────────────────────────────────────────────────────┤
  │                                                                      │
  │  logs                         log_analytics                         │
  │  ─────────────────────        ────────────────────────────          │
  │  id (PK)                      id (PK)                               │
  │  service_id ◄── KEY           service_id ◄── KEY                   │
  │  host_id                      endpoint                              │
  │  timestamp                    method                                │
  │  log_level                    status_code                           │
  │  raw_message                  latency_ms                            │
  │  parsed_json                  client_ip                             │
  │                               is_error                              │
  │                               is_probe                              │
  │                               ts                                    │
  │                                                                      │
  │  analytics_summary                                                   │
  │  ─────────────────────────────────────                               │
  │  id (PK)                                                             │
  │  service_id ◄── KEY                                                  │
  │  hour_bucket                                                         │
  │  req_count · error_count                                             │
  │  p50_ms · p95_ms · p99_ms                                           │
  │  tps_avg · tps_peak                                                  │
  │  top_endpoints (JSON)                                                │
  └──────────────────────────────────────────────────────────────────────┘

  ┌──────────────────────────────────────────────────────────────────────┐
  │                     INFRASTRUCTURE TABLES                            │
  ├──────────────────────────────────────────────────────────────────────┤
  │                                                                      │
  │  infra_metrics_latest         mysql_monitor_latest                  │
  │  ─────────────────────        ────────────────────                  │
  │  host_id (FK)                 host_id (FK)                          │
  │  cpu_pct                      slow_queries                          │
  │  mem_pct                      conn_count                            │
  │  disk_pct                     replication_lag                       │
  │  load_1m / 5m / 15m           innodb_hit_rate                       │
  │  ts                           ts                                    │
  └──────────────────────────────────────────────────────────────────────┘

  ┌──────────────────────────────────────────────────────────────────────┐
  │                    OPERATIONS TABLES                                 │
  ├──────────────────────────────────────────────────────────────────────┤
  │                                                                      │
  │  alerts           alert_rules        audit_log                      │
  │  ─────────────    ─────────────────  ──────────────────             │
  │  id               id                 id                             │
  │  rule_id (FK)     metric             user_id                        │
  │  service_id       operator           action                         │
  │  severity         threshold          resource                       │
  │  message          window_mins        old_value                      │
  │  acked            notify_channels    new_value                      │
  │  acked_by         enabled            ip_address                     │
  │  ts               ts                 ts                             │
  │                                                                      │
  │  incident_entries    rfc_entries    managed_service_tickets         │
  │  server_inventory    team_members   timesheet_entries               │
  └──────────────────────────────────────────────────────────────────────┘
```

---

## 🔌 API Reference

### Analytics Group

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/analytics/overview` | Request volume, error rate, status distribution |
| `GET` | `/api/analytics/paths` | Top endpoint breakdown |
| `GET` | `/api/analytics/hourly` | Hourly traffic time series |
| `GET` | `/api/analytics/status` | HTTP status code distribution |
| `GET` | `/api/analytics/exceptions` | Exception type trends |
| `GET` | `/api/analytics/response-times` | Latency percentiles (p50/p95/p99) |
| `GET` | `/api/analytics/endpoint-tps` | Per-endpoint TPS trend |
| `GET` | `/api/analytics/summary` | Aggregated KPI summary |
| `GET` | `/api/analytics/executive` | Executive summary view |
| `GET` | `/api/analytics/service-groups` | Service group breakdown |
| `GET` | `/api/analytics/ips` | Top client IP analysis |
| `GET` | `/api/analytics/methods` | HTTP method distribution |
| `GET` | `/api/analytics/probes-summary` | Business vs probe traffic |
| `GET` | `/api/analytics/tps-summary` | TPS aggregate summary |
| `POST` | `/api/analytics/backfill` | Trigger analytics backfill job |

> All analytics endpoints accept `?service_id=` for microservice-scoped queries.

### Logs & Ingestion Group

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/logs` | Paginated log query with filters |
| `GET` | `/api/logs/export` | Export logs as CSV |
| `GET` | `/api/logs/stream` | SSE real-time log stream |
| `POST` | `/api/import` | Trigger SSH import for one host |
| `POST` | `/api/import/all` | Trigger SSH import for all hosts |
| `GET` | `/api/import/status/:job_id` | Poll async import job status |

### Services & Config Group

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/services` | List all registered services |
| `GET` | `/api/config/services` | Service config with deployments |
| `POST` | `/api/config/service` | Create or update a service |
| `GET` | `/api/hosts` | List all registered hosts |
| `POST` | `/api/config/host` | Create or update a host |
| `GET` | `/api/config/modules` | List configured modules |

### Alerts & RCA Group

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/alerts` | List active alerts |
| `GET` | `/api/alerts/rules` | List alert rules |
| `PUT` | `/api/alerts/:id/ack` | Acknowledge an alert |
| `POST` | `/api/rca/analyze` | Run RCA analysis for a service |
| `GET` | `/api/infra/metrics/latest` | Latest infra metrics snapshot |
| `POST` | `/api/infra/metrics/:host_id/run` | Force infra collection run |

### Planned Service-Scoped Endpoints *(Roadmap)*

```
GET  /api/analytics/service/:id/overview
GET  /api/analytics/service/:id/endpoints
GET  /api/analytics/service/:id/latency
GET  /api/analytics/service/:id/exceptions
GET  /api/analytics/service/:id/ips
GET  /api/deployments
GET  /api/deployments/:id
```

---

## 🖥 Frontend Pages

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                          20+ OPERATIONAL PAGES                              │
├──────────────────────────────────┬──────────────────────────────────────────┤
│  OBSERVABILITY                   │  OPERATIONS & ITSM                       │
├──────────────────────────────────┼──────────────────────────────────────────┤
│  /master      Master Portal NOC  │  /incidents   Incident Management        │
│  /analytics   Trend Analysis     │  /rfc         RFC Tracker                │
│  /logs        Log Viewer         │  /automation  Automation Hub             │
│  /live-logs   Real-time Stream   │  /billing     Billing Portal             │
│  /infra       Infra Dashboard    │  /ngw         NGW Management             │
│  /alerts      Alert Manager      │  /sap         SAP Integration            │
│  /rca         RCA Analysis       │  /team        Team Directory             │
│  /db-monitor  DB Observability   │  /timesheet   Timesheet                  │
│                                  │  /inventory   Server Inventory           │
│  ADMINISTRATION                  │  /managed     Managed Service Tickets    │
├──────────────────────────────────┤                                          │
│  /config      Platform Config    │  SERVICE VIEWS                           │
│  /admin       Admin Centre       ├──────────────────────────────────────────┤
│  /audit       Audit Trail        │  /service/:id  Service Detail Page       │
│  /permissions Permission Matrix  │  /module/:id   Module Detail Page        │
└──────────────────────────────────┴──────────────────────────────────────────┘
```

---

## ✨ Feature Highlights

### 🔍 End-to-End Observability
Full telemetry pipeline: raw log line → parsed fact → hourly aggregate → service KPI → dashboard. Every stage carries `service_id` for true microservice isolation.

### ⚡ Real-time Log Streaming
Live tail delivered over **Server-Sent Events (SSE)** with per-service and per-level filtering. Zero polling — inotify-driven push from the watcher thread.

### 🧠 Rule-Based RCA Engine
Correlates error spikes, latency anomalies, and infrastructure health signals into ranked root cause hints. Configurable rule weights and lookback windows.

### 🏗 Service-First Architecture
`service_id` is wired into every table, every query, and every API parameter. Multi-service deployments on shared hosts are fully separated at the query level.

### 📊 Rich Analytics Suite
- TPS with peak detection
- Latency percentiles: p50 / p95 / p99
- Endpoint breakdown with top-N ranking
- Error rate and exception type distribution
- Client IP analysis and consumer patterns
- Business traffic vs probe traffic separation
- Hourly traffic heatmaps

### 🛡 Enterprise RBAC
Fine-grained role-based access with project-scoped permissions, a full audit trail on every mutation, and session lifecycle management.

### 🔔 Smart Alerting
Configurable threshold rules across any metric. Multi-channel notification via SMTP and webhooks. Keyword-triggered escalation emails. Full acknowledgment workflow.

### 🏎 Resilience Layer
Circuit breakers, exponential backoff retries, async import queue, rate limiting, and system health monitoring are built into `core/resilience.py` — not bolted on.

### 🗄 DB Portability
Seamless MySQL/SQLite abstraction in `core/db_backend.py`. All schema migrations, bootstrap, and CRUD operations work identically on both backends. Zero code changes to switch.

---

## ⚡ Performance Strategy

```
BACKEND
  • service_id filter on every analytics SQL path
  • Short-TTL API cache on hot portal + analytics reads
  • Aggregate tables for hourly summaries (avoid full-table scans)
  • Cap expensive list queries, load-more on demand
  • Async import queue — ingestion never blocks the UI path

DATABASE
  • Indexes: host_id · ts · endpoint · status · latency · client_ip
  • service_id composite indexes on log_analytics + analytics_summary
  • Retention-aware purge jobs (scheduled, off critical path)
  • mysql_monitor_history for DB health trending without app overhead

FRONTEND
  • Lazy-load deep tabs — only render visible chart panels
  • Debounced search and typeahead (no per-keystroke queries)
  • Paginate heavy log and endpoint tables
  • Only instantiate Chart.js for visible mini-charts
  • Chunked Master Portal rendering — cards stream in progressively
```

---

## 🔒 Security & RBAC

```
┌─────────────────────────────────────────────────────────────┐
│                     RBAC ARCHITECTURE                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   Request ──► Auth Decorator ──► Session Check             │
│                     │                                       │
│                     ▼                                       │
│            Role Lookup (core/rbac.py)                       │
│                     │                                       │
│          ┌──────────┴──────────┐                            │
│          ▼                     ▼                            │
│    Permission Matrix      Project Scope                     │
│    (action × resource)    (per-project)                     │
│          │                     │                            │
│          └──────────┬──────────┘                            │
│                     ▼                                       │
│            Route Access Granted                             │
│                     │                                       │
│                     ▼                                       │
│            Audit Log Entry Written                          │
│          (user · action · resource · ip · ts)               │
└─────────────────────────────────────────────────────────────┘

ROLES:  Admin · Operator · Viewer · Service-Owner (WIP)
AUDIT:  Every create / update / delete writes to audit_log
RATE:   Per-route rate limiting via core/resilience.py
```

---

## 🚀 Quick Start

### Prerequisites

```bash
Python 3.11+
MySQL 8.x  (or SQLite for local dev)
```

### Install

```bash
git clone https://github.com/your-org/opscore-observability.git
cd opscore-observability

python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate

pip install -r requirements.txt
```

### Configure

```bash
cp config.example.yaml config.yaml
```

```yaml
# config.yaml
database:
  backend:  mysql          # or: sqlite
  host:     localhost
  port:     3306
  name:     opscore
  user:     opscore_user
  password: your-password

smtp:
  host:     smtp.example.com
  port:     587
  from:     alerts@example.com
  user:     alerts@example.com
  password: your-smtp-password

platform:
  secret_key:  change-this-in-production
  debug:       false
  log_level:   INFO
```

### Bootstrap & Run

```bash
# Bootstrap database schema
python -m core.db_bootstrap

# Start the platform
python app.py

# Open in browser
open http://localhost:5000/master
```

### First Steps

```
1. Navigate to /config
2. Add a host (hostname + SSH credentials)
3. Register a service (name + type + SLA tier)
4. Create a deployment (bind service → host → log path)
5. Trigger an import: POST /api/import
6. Watch logs appear at /logs and /live-logs
7. Check analytics at /analytics?service_id=<your-service>
```

---

## 🗺 Roadmap

### Phase 1 — Service Scoping *(in progress)*
- [x] `service_id` in logs, log_analytics, analytics_summary
- [x] Service-aware SSH importer and log watcher
- [x] Service-scoped Trend Analysis parameter resolution
- [x] Service aggregate rebuild + scheduler job
- [x] Service-first Master Portal cards
- [ ] Explicit `/api/analytics/service/:id/*` endpoints
- [ ] Extract remaining route groups from `app.py`

### Phase 2 — Topology & SLO *(planned)*
- [ ] Service topology / dependency graph view
- [ ] SLO / SLA definition and burn-rate tracking
- [ ] HA cluster health panels
- [ ] Service-to-service latency correlation

### Phase 3 — Intelligence *(planned)*
- [ ] Anomaly detection (statistical baseline + deviation alerts)
- [ ] Alert grouping and correlation engine
- [ ] RCA scorecard with confidence scoring
- [ ] Distributed trace / span model

### Phase 4 — Scale *(planned)*
- [ ] Long-term retention with tiered storage
- [ ] High-volume pagination across all heavy queries
- [ ] Streaming aggregation (bypass batch jobs)
- [ ] Multi-region / multi-cluster support

---

## 🧪 Validation Sequence

```bash
# Recommended smoke-test sequence after a fresh deploy

1.  Create a service via /config
2.  Add a host and bind SSH credentials
3.  Create a deployment (service → host → log_path)
4.  POST /api/import  → verify job_id returned
5.  GET  /api/import/status/:job_id  → poll until complete
6.  GET  /api/logs?service_id=<id>  → confirm rows with service_id set
7.  GET  /analytics  → verify Trend Analysis renders service data
8.  GET  /infra  → confirm host metrics collected
9.  Trigger a threshold breach → confirm alert fires
10. Check /audit  → confirm actions logged
```

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

<div align="center">

```
Built for SREs · NOC Teams · Platform Engineers
```

**OpsCore Observability Intelligence**
*The fastest path to Dynatrace-grade operations without the Dynatrace bill.*

</div>
