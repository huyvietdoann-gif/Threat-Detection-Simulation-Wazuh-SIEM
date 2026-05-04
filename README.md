# 🛡️ Mini SOC Lab – Threat Detection & Simulation with Wazuh SIEM

![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)
![SIEM](https://img.shields.io/badge/SIEM-Wazuh%204.7-blue)
![Framework](https://img.shields.io/badge/Framework-MITRE%20ATT%26CK-red)
![Platform](https://img.shields.io/badge/Platform-VMware%20%2F%20VirtualBox-lightgrey)

> A hands-on Security Operations Center (SOC) lab environment built for threat detection, log analysis, and attack simulation using the MITRE ATT&CK framework.

---

## 📌 Project Overview

This project builds a small-scale SOC environment designed for hands-on practice and personal portfolio demonstration. The system integrates **Wazuh SIEM** to collect and analyze logs from multiple endpoints, combined with **Atomic Red Team** to simulate real-world attack techniques mapped to the MITRE ATT&CK framework.

### Objectives

- Deploy and configure Wazuh SIEM (all-in-one deployment)
- Collect logs from multiple sources: Windows Event Log, Sysmon, Linux Syslog/Auditd
- Build custom decoders and detection rules mapped to MITRE ATT&CK techniques
- Simulate real-world attack scenarios using Atomic Red Team across multiple tactics
- Evaluate detection rate and visualize security events on Kibana dashboard

### Technologies Used

| Component | Tool | Version |
|---|---|---|
| SIEM | Wazuh | 4.7.x |
| Indexer / Dashboard | Elastic Stack (Wazuh fork) | 4.7.x |
| Endpoint Monitoring | Sysmon | Latest |
| Attack Simulation | Atomic Red Team | Latest |
| Framework | MITRE ATT&CK | v14 |

---

## 🖧 Lab Architecture

```
                    ┌─────────────────────┐
                    │   Kibana Dashboard  │
                    │   SOC Analyst View  │
                    └──────────┬──────────┘
                               │ alerts
                    ┌──────────▼──────────┐
                    │    Wazuh Server     │
                    │   Ubuntu 22.04      │
                    │   IP: 10.10.0.6     │
                    └───┬─────────────┬───┘
               logs ◄───┘             └───► logs
    ┌──────────────────┐           ┌──────────────────┐
    │  Windows 10      │           │  Ubuntu 20.04    │
    │  IP: 10.10.0.7   │           │  IP: 10.10.0.4   │
    │  - Sysmon        │           │  - Wazuh Agent   │
    │  - Wazuh Agent   │           │  - Auditd        │
    │  - Atomic RT     │           │  - Atomic RT     │
    └────────▲─────────┘           └────────▲─────────┘
             │  attack (simulated)           │
             └──────────────┬───────────────┘
                   ┌────────┴────────┐
                   │  Kali Linux     │
                   │  IP: 10.10.0.x  │
                   │  (Attacker)     │
                   └─────────────────┘

Network: 10.10.0.0/24 (Internal Lab Network)
```


<img width="1024" height="664" alt="project topo" src="https://github.com/user-attachments/assets/6b3a2d19-2107-44d3-b116-4f8fbbf33cb5" />

### VM Specifications

| VM | OS | IP | RAM | CPU | Role |
|---|---|---|---|---|---|
| Wazuh Server | Ubuntu 22.04 LTS | 10.10.0.6 | 4GB | 2 core | SIEM, Indexer, Dashboard |
| Windows Agent | Windows 10 | 10.10.0.7 | 4GB | 2 core | Endpoint (Sysmon + Atomic RT) |
| Linux Agent | Ubuntu 20.04 | 10.10.0.4 | 2GB | 2 core | Endpoint (Auditd + Atomic RT) |
| Kali Attacker | Kali Linux | 10.10.0.x | 4GB | 2 core | Attack simulation |

---

## 📂 Documentation

| Phase | Description | Status |
|---|---|---|
| [Phase 1 – Infrastructure](docs/phase1-infrastructure.md) | Deploy Wazuh Server, configure VMs | 🔄 In Progress |
| [Phase 2 – Agent & Log Collection](docs/phase2-agent-log-collection.md) | Install agents, configure log sources | ⏳ Pending |
| [Phase 3 – Log Parsing](docs/phase3-log-parsing.md) | Write custom decoders | ⏳ Pending |
| [Phase 4 – Detection Rules](docs/phase4-detection-rules.md) | Write MITRE-mapped detection rules | ⏳ Pending |
| [Phase 5 – Atomic Simulation](docs/phase5-atomic-simulation.md) | Run Atomic Red Team tests | ⏳ Pending |

---

## 📁 Repository Structure

```
mini-soc-lab/
├── README.md
├── docs/
│   ├── phase1-infrastructure.md
│   ├── phase2-agent-log-collection.md
│   ├── phase3-log-parsing.md
│   ├── phase4-detection-rules.md
│   └── phase5-atomic-simulation.md
├── configs/
│   ├── ossec.conf
│   ├── custom_decoders.xml
│   └── local_rules.xml
├── screenshots/
│   └── (per-phase screenshots)
└── atomic-tests/
    └── test-results.md
```

---

## 🚀 Quick Start

```bash
# 1. Clone this repo
git clone https://github.com/<username>/mini-soc-lab.git

# 2. Follow Phase 1 to set up the infrastructure
# See: docs/phase1-infrastructure.md

# 3. Deploy Wazuh (all-in-one)
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
curl -sO https://packages.wazuh.com/4.7/config.yml
sudo bash wazuh-install.sh --wazuh-indexer node-1
sudo bash wazuh-install.sh --wazuh-server wazuh-1
sudo bash wazuh-install.sh --wazuh-dashboard dashboard
```

---

## 🎯 MITRE ATT&CK Coverage

| Tactic | Technique | Atomic Test | Detection Rule |
|---|---|---|---|
| Credential Access | T1003 – OS Credential Dumping | ✅ | ⏳ |
| Execution | T1059.001 – PowerShell | ✅ | ⏳ |
| Credential Access | T1110.001 – Password Brute Force | ✅ | ⏳ |
| Persistence | T1053.005 – Scheduled Task | ✅ | ⏳ |
| Defense Evasion | T1055 – Process Injection | ✅ | ⏳ |

---

## 👤 Author

**Huy** – Cybersecurity Student, Year 4  
Focus: SOC, SIEM, Threat Detection, Blue Team

---

*This project is for educational and portfolio purposes only. All attack simulations are performed in an isolated lab environment.*
