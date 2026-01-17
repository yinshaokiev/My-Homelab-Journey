# 🛡️ Project: Enterprise SIEM Setup (Splunk)

**Date:** January 16, 2026
**Status:** ✅ Operational
**Environment:** Proxmox Home Lab (Linux VM)

## 🎯 Objective
To deploy and configure **Splunk Enterprise** as a centralized Security Information and Event Management (SIEM) system within my home lab. The goal was to establish log ingestion, configure a "Gold Image" server, and practice troubleshooting real-world resource constraints.

## 🛠️ Tech Stack
* **Hypervisor:** Proxmox VE
* **OS:** Linux (Debian/Ubuntu based)
* **Software:** Splunk Enterprise 9.x
* **Protocol:** SSH (Remote Management)

## 📝 Implementation Steps

### 1. Installation & Boot Configuration
Downloaded the `.deb` package and installed it via the command line. Configured Splunk to start automatically when the server reboots.

```bash
# Unpack and install
sudo dpkg -i splunk-*.deb

# Enable boot-start so it survives reboots
sudo /opt/splunk/bin/splunk enable boot-start
``

