# 🐉 Kali Linux Lab Network Reconnaissance

| Parameter | Details |
| :--- | :--- |
| **Date** | January 11, 2026 |
| **Platform** | Proxmox VE (Virtual Machine) |
| **Objective** | Perform initial network reconnaissance on local infrastructure. |

* **VM ID:** 103
* **OS:** Kali Linux (Debian-based)
* **Desktop Environment:** Xfce (Selected for low resource usage)
* **Network:** Bridged Mode (Connected to home LAN `10.0.0.x`)

## **Phase 1:** Host Discovery (ping sweep) 
* **Goal:** Identify active devices on the local `10.0.0.x/xx` network without triggering detialed services scans.
  ```bash
  sudo nmap -sn 10.0.0.x/xx
  ```
  **Results:**
  Successfully mapped the nework topology
  * infrastructure identified:
    * `10.0.0.1` (Gateway/Router)
    * `10.0.0.xxx` (Proxmox Host)
    * `10.0.0.xxx` (Pi-hole DNS server
  * IoT & Clients: Identified various devices including security cameras (Blink), gaming consoles, and smart plugs via MAC address vendor lookup.

## **Phase 2:** Vulnerability Assessment (Service Scanning)
* **Goal:** Perform "Banner Grabbing" on the local Pi-hole server to identify open ports and service versions.
  ```bash
  sudo nmap -sV -p- 10.0.0.xxx
  ```
  * `-sV`: Service Version Detection
  * `-p-`: Scan all 65,535 ports
    
  **Findings:**
  | Port | Service | Version Detected | Status | | :--- | :--- | :--- | :--- | | 22 | SSH | OpenSSH 10.0p2 | Open | | 53 | DNS | dnsmasq 2.92test21 (pi-hole) | Open | | 80 | HTTP | lighttpd | Open | | 443 | HTTPS | lighttpd | Open |

  **Analysis:** The server is exposing standard administration ports. The SSH version is current, and the specific dnsmasq version confirms the device is running Pi-hole.

  ## **Phase 3:** Router OS Fingerprinting
  * **Goal:** Analyze the "Black Box" gateway (`10.0.0.1`) to determine its Operating System and firewall rules.
    ```bash
    sudo nmap -O 10.0.0.1
    ```
  **Findings:**
    * OS Detected: Linux 5.X Kernel.
    * Firewall Behavior:
      * Ports 22 (SSH), 23 (Telnet), and 8080 are `filtered` (packets dropped), indicating a firewall is actively blocking management access from the LAN.
      * Ports 80/443 are open for the web configuration interface.

## **Skills Demonstrated**
* **Virtualization:** ISO deployment, QEMU agent configuration, Snapshot management.
* **Network Reconnaissance:** Nmap scanning (Ping sweeps, SYN scans).
* **Analysis:** Interpreting TCP/IP handshakes, TTL values, and banner data.
* **Security Assessment:** Identifying open attack surfaces on local servers.
