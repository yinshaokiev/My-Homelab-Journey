# 🛡️ Blue Team Infrastructure: SIEM Server
**Date:** January 16, 2026
**Component:** VM 104 (BlueTeam-SIEM)
**Role:** Central Logging & Threat Detection (The Watchtower)

---

## 🏗️ System Specifications
* **Hostname:** `siem-server`
* **OS:** Ubuntu Server 24.04 LTS
* **IP Address:** `10.0.0.34` (Currently Dynamic)
* **Software:** Splunk Enterprise 9.x
* **Resources:**
    * **Storage:** 40GB Virtual Disk (Configured with low-space workarounds)
    * **RAM:** 4GB
    * **Network:** Bridged Adapter (Access to Home Network)

---

## 🛠️ Installation Log

### Phase 1: Virtual Machine Creation ✅
* **Hypervisor:** Proxmox VE
* **VM ID:** 104
* **Status:** Operational.

### Phase 2: OS Configuration ✅
* **User Account:** `admin_ysv`
* **SSH Server:** **Enabled** (Verified connection via Terminal).

### Phase 3: SIEM Deployment (Splunk) ✅
* **Installation:** Installed Splunk Enterprise via `.deb` package.
* **Boot Config:** Enabled boot-start so the service survives reboots.
* **Privileges:** Configured service to run as root (`--run-as-root`) to ensure full access to system logs.
* **Data Ingestion:** Successfully configured the first input to monitor local `/var/log` files.
<img width="3827" height="1757" alt="Screenshot 2026-01-16 200050" src="https://github.com/user-attachments/assets/3438a6fa-6faf-4b27-89ae-126e5cd598db" />

---

## ⏳ Next Steps (To Do)
- [ ] **Static IP:** Lock the IP address (currently `10.0.0.34`) in the router or VM config so it doesn't change.
- [ ] **Universal Forwarders:** Install the lightweight Splunk agent on the Fedora Laptop to forward logs here.
- [ ] **Kali Linux Integration:** Forward logs from the Kali VM (`103`) to detect attack signatures.
- [ ] **Dashboards:** Create a visual map of SSH login attempts.

---

## 📝 Notes & Observations
* **Current State:** The SIEM is live and ingesting its own internal logs.
* **Validation:** Verified functionality by searching `index=*` and seeing live events in the "Search & Reporting" app.
* **Shutdown Procedure:** Verified safe shutdown using `sudo poweroff` via SSH to protect the database.

---
## 🔗 Navigation
* [🏠 Back to Main Menu](../01-HomeLab_Journey/01-README.md)
