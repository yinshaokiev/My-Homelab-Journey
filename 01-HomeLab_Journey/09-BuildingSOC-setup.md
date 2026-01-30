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
---

* **Kali Linux (Forwarder)
The Universal Forwarder is installed to monitor system logs and send them to the splunk server
* Monitor file: `/var/log/auth.log` (Tracks SSH logins, sudo usage, and failed passwords).
* Forwarder Control:
  ```bash
  sudo /opt/splunkforwarder/bin/splunk restart
  ```
## ⚔️ Simulation Field Manual
Use these steps to re-run the attack simulation and verify detection.

## 🟢 Scenario: SSH Brute Force Attack
Objective: Simulate an attacker attempting to guess passwords via SSH.

Step 1: Generate "Noise" (On Kali Linux)
* Open the Terminal.
* Attempt to login with a non-existent user:
```bash
ssh badguy@localhost
```
* when prompted for password:
  * type any random password (e.g., `wrongpass1`).
  * hit enter
* repeat 3-5 times to generate multiple failure events
* press `Ctrl + C` to exit
* (note: if you get "Connection Refused, "ensure SSH is running : `sudo systemctl start ssh`)

Step 2: Hunt the Logs (go to Splunk Interface)
* Navigate to Search & Reporting
* Set the Time Picker to "Last 15 min".
* run the following SPL ( Search Processing Language) query:
  ```Code snippet
  index=main "Failed password"
  ```
* Expected Results: You should see multiple events listed as:
  * Failed password for invalid user badguy from ::1port X ssh2
 ---
## 📝 Troubleshooting & Maintenance
Common Issues
* Splunk Alert: "IOWait"
   * Cause: Virtual Machine disk speed is slower than enterprise hardware.
   * Action: Safe to ignore in a home lab environment.

*Missing Logs?
   * Check if the Forwarder is running on Kali:
```bash
sudo /opt/splunkforwarder/bin/splunk status
```
   * Verify the log files exists:
```bash
ls -l /var/log/auth.log
```
  
---
## 🚀 Future Roadmap
* [ ] Dashboards: Create a visual map of attack origins.
* [ ] Alerts: Configure email notifications for repeated login failures.
* [ ] Windows Expansion: Add a Windows 11 Victim machine and install Sysmon.

---
## 🔗 Navigation
* [🏠 Back to Main Menu](../01-HomeLab_Journey/01-README.md)
