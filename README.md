# ELK-Based Threat Detection SIEM

A self-hosted SIEM built from scratch using the ELK Stack (Elasticsearch, Logstash, Kibana) and Filebeat, containerized with Docker. Ingests system and network logs, parses and indexes them for real-time search, and applies threat detection rules to surface suspicious activity.

## What It Does

- Collects system logs from a Ubuntu host using Filebeat
- Ships logs through Logstash pipelines for parsing and normalization
- Indexes structured events in Elasticsearch for fast search and correlation
- Visualizes activity and alerts in Kibana dashboards
- Applies detection rules to flag anomalous behavior (failed logins, port scans, unusual process activity)

## Architecture

```
Ubuntu Host Logs
      │
      ▼
  Filebeat (log shipper)
      │
      ▼
  Logstash (parse + normalize)
      │
      ▼
Elasticsearch (index + store)
      │
      ▼
  Kibana (dashboards + alerts)
```

## Stack

| Component       | Role                              |
|----------------|-----------------------------------|
| Elasticsearch   | Log storage and search engine     |
| Logstash        | Log parsing and pipeline          |
| Kibana          | Dashboards and visualization      |
| Filebeat        | Log collection from Ubuntu host   |
| Docker Compose  | Container orchestration           |

## Setup

### Prerequisites
- Docker and Docker Compose installed
- Ubuntu host (tested on Ubuntu 22.04)

### Run

```bash
git clone https://github.com/aaminasultan19/ELK-based-apt-detection.git
cd ELK-based-apt-detection
docker compose up -d
```

Access Kibana at `http://localhost:5601`

### Filebeat Configuration

Filebeat is configured via `filebeat.yml` to monitor system log paths and forward to Logstash. Edit the `paths` section to point to your log sources.

## Detection Rules

Threat detection rules are applied in Kibana to flag:

- Repeated failed SSH login attempts (brute-force indicator)
- Unusual outbound connections (potential C2 communication)
- High-frequency port activity (port scan pattern)
- Processes spawned from unexpected parent processes

## Log Sources

- `/var/log/syslog` — general system events
- `/var/log/auth.log` — authentication and sudo activity
- `/var/log/kern.log` — kernel-level events

## Skills Demonstrated

- SIEM architecture and deployment from scratch
- Log ingestion pipeline design (Filebeat → Logstash → Elasticsearch)
- Threat detection rule creation
- Security event visualization with Kibana
- Docker-based infrastructure setup
- SOC analyst workflow simulation

## Context

Built as a hands-on project to understand how enterprise SIEM systems work — from log collection and normalization through to threat detection and alert triage. Modeled on real SOC workflows.
