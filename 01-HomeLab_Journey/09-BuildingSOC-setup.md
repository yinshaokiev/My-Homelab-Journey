# 🛡️ Home Lab: Building a SOC with Splunk & Kali Linux

## 📖 Project Overview
This project focuses on building a home-based **Security Operations Center (SOC)** to simulate cyber attacks and detect them using enterprise-grade tools. The goal is to gain hands-on experience with **Log Analysis**, **SIEM Configuration**, and **Threat Hunting**.

### 🏗️ Network Architecture
* **Hypervisor:** Proxmox VE (Bare Metal)
* **SIEM Server (The Watchtower):**
    * **OS:** Ubuntu Server 24.04
    * **Software:** Splunk Enterprise
    * **IP:** `10.0.0.34`
* **Attacker (The Red Team):**
    * **OS:** Kali Linux
    * **Software:** Splunk Universal Forwarder
    * **Role:** Generates attack traffic and forwards logs to the SIEM.

---

## ⚙️ Configuration Details

### 1. Splunk Enterprise (Server)
Configured to receive data on port **9997** from external forwarders.
* **Web Interface:** `http://10.0.0.34:8000`
* **Service Control:**
  ```bash
  sudo /opt/splunk/bin/splunk start
  sudo /opt/splunk/bin/splunk status
  ```

  
