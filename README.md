# 🛡️ EDR Implementation with Wazuh 4.14.2

> Blue Team Project | Sistem Endpoint Detection & Response

![Wazuh](https://img.shields.io/badge/Wazuh-4.14.2-blue)
![Sysmon](https://img.shields.io/badge/Sysmon-v15.15-green)
![Windows](https://img.shields.io/badge/Windows-10-blue)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

## 📋 Overview

Proyek ini membangun sistem EDR sederhana untuk **kantor kecil (15 komputer)**
yang mengalami masalah malware. Sistem dapat memonitor aktivitas endpoint
secara real-time dan mendeteksi behavior mencurigakan sebelum terlambat.

## 🏗️ Arsitektur

```text
Laptop Host
├── VM 1 → Wazuh Server (Manager + Indexer + Dashboard)
├── VM 2 → Windows 10 Endpoint (Wazuh Agent + Sysmon v15.15)
└── VM 3 → Ubuntu Desktop (Wazuh Agent)
Semua terhubung via ZeroTier (10.75.139.146)
```

## 🎯 Detection Results

| # | Skenario | MITRE | Rule ID | Level | Status |
|---|----------|-------|---------|-------|--------|
| 1 | EICAR Test File | T1204 | 62123 | 12 | ✅ Detected |
| 2 | LSASS Memory Dump | T1003.001 | 92900 | 12 | ✅ Detected |
| 3 | SAM Database Dump | T1003.002 | 62123 | 12 | ✅ Detected |
| 4 | Suspicious PowerShell | T1059.001 | 92066 | 4 | ✅ Detected |
| 5 | Persistence via Registry | T1547.001 | 60112 | 8 | ✅ Detected |
| 6 | New Service Created | T1543.003 | 61138 | 5 | ✅ Detected |
| 7 | WMI Parent-Child | T1047 | 100011 | 12 | ✅ Detected |
| 8 | LOLBIN Certutil Abuse | T1218 | 62123 | 12 | ✅ Detected |
| 9 | Discovery Activity | T1082 | 92031 | 3 | ✅ Detected |

> **9/9 skenario terdeteksi** — melebihi target minimum 3 dari 5

## 📸 Screenshots

### Dashboard Overview
![Dashboard](screenshots/01-dashboard-overview.png)

### LSASS Credential Dump Detection
![LSASS](screenshots/03-lsass-detection.png)

### EICAR Malware Detection  
![EICAR](screenshots/04-eicar-detection.png)

### Mimikatz SAM Dump — Trojan:Win32/RegistryExfil.A
![SAM](screenshots/05-mimikatz-sam-dump.png)

## 🔧 Tools & Configuration

| Tool | Version | Role |
|------|---------|------|
| Wazuh | 4.14.2 | SIEM + EDR Platform |
| Sysmon | v15.15 | Windows Event Logging |
| ZeroTier | Latest | Private Overlay Network |
| Windows Defender | 4.18.26030.3011 | AV Layer |

```markdown
## 📁 Repository Structure

├── screenshots/     # Evidence dari semua deteksi
├── configs/         # Sysmon config + Wazuh custom rules
├── docs/            # Technical report & playbook
└── report/          # Final technical report (.docx)
```

## 👥 Tim

| Role | Tugas |
|------|-------|
| Host | Setup VM, network, snapshot & backup |
| Detection & Forensik | Rules, query hunting, testing, export log |
| Endpoint Security | Install Wazuh server & agent, dashboard |
| Red Team Simulator | EICAR, Atomic Red Team, koordinasi testing |
| Analyst Forensik | Analisis, timeline, laporan |
| Dokumentasi | Laporan & slide presentasi |

## 📄 License
MIT License — For educational purposes only
