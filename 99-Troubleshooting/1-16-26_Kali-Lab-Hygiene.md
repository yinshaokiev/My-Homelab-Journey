# 🛡️ Home Network Hygiene Report
**Date:** January 16, 2026  
**Auditor:** Yinshaokie Solomon Vang  
**Tools Used:** Proxmox VE, Kali Linux (VM), Nmap

---

## 🎯 Objective
To perform a "Network Hygiene Check" on the local home network (`10.0.0.0/24`) to identify rogue devices, open ports, and potential security vulnerabilities on key infrastructure.

---

## 🔍 Phase 1: Network Discovery
**Goal:** Identify active devices on the network.

* **Command:**
    ```bash
    ip a  # Verified Attacker IP
    sudo nmap -sn 10.0.0.0/24
    ```
* **Findings:**
    * Network Range: `10.0.0.0/24`
    * Active Hosts: ~15 devices detected (IoT, Personal Devices, Servers).
    * **Status:** No rogue MAC addresses or unrecognized manufacturers detected.

---

## 🖥️ Phase 2: Windows PC Security Audit
**Target:** Main Workstation
**IP:** `10.0.0.xxx` (Workstation)

* **Command:**
    ```bash
    sudo nmap -sV -O 10.0.0.xxx
    ```
* **Results:**
    * **Status:** ✅ **PASSED (Stealth Mode)**
    * **Port State:** `All 1000 scanned ports ... are in ignored states.`
    * **Analysis:** Windows Firewall is correctly configured to "Block/Filter" unsolicited traffic. The workstation is effectively invisible to network scans.

---

## 📂 Phase 3: NAS (Network Attached Storage) Audit
**Target:** Proxmox LXC Container
**IP:** `10.0.0.xxx` (NAS)

* **Command:**
    ```bash
    sudo nmap -sV 10.0.0.xxx
    ```
* **Results:**
    * **Status:** ✅ **PASSED (Normal Service Profile)**
    * **Open Ports:**
        * `22/tcp` (OpenSSH): Secured via Strong Password.
        * `80/tcp` (HTTP): Web Interface.
        * `111/tcp` (rpcbind): NFS Service.
        * `139, 445/tcp` (Samba): Local File Sharing (SMB).
        * `5357/tcp` (WSDD): Windows Service Discovery.
    * **Analysis:** Only necessary services for file sharing are active. No insecure protocols (FTP/Telnet) detected.

---

## ✅ Conclusion
The local network perimeter is secure.
1.  **Workstation:** Highly secure (Filtered).
2.  **Server/NAS:** Functioning normally with expected services.
