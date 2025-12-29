# 🛡️ Personal Cybersecurity & Networking Home Lab
### **Proxmox | Tailscale | Pi-hole | Sec+ & Net+ Roadmap**

![Proxmox](https://img.shields.io/badge/Proxmox-812921?style=for-the-badge&logo=proxmox&logoColor=white)
![Tailscale](https://img.shields.io/badge/Tailscale-4433E1?style=for-the-badge&logo=tailscale&logoColor=white)
![Pi-hole](https://img.shields.io/badge/Pi--hole-96060C?style=for-the-badge&logo=pi-hole&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E9430F?style=for-the-badge&logo=ubuntu&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

> **🚀 Learning Journey:** This repository is my step-by-step learning process for setting up my very own home lab for practicing **CompTIA Security+** and **Network+** concepts. It serves as a living document of my progress, troubleshooting, and architectural growth.

---

## 🏗️ Architecture & Topology
My lab is built on a **"Hardened Hardware"** model using an ASUS laptop as a dedicated hypervisor. 

### **Logical Infrastructure**
* **Hypervisor:** Proxmox VE 8.x
* **Identity & Access (IAM):** Tailscale Mesh VPN (OIDC via Google/MFA)
* **Defense in Depth:** Pi-hole DNS Firewall (LXC)
* **Remote Management:** Secure Tailscale Tunnel (No Open Ports)

---

## 🛠️ Current Services & Tech Stack
| Service | Environment | Function | Certification Focus |
| :--- | :--- | :--- | :--- |
| **Pi-hole** | LXC Container | DNS Sinkhole | **Sec+:** Content Filtering / **N+:** DNS Protocols |
| **Tailscale** | LXC Container | Mesh VPN | **Sec+:** Zero Trust / **N+:** VPN Topologies |
| **Ubuntu Host** | VM | Docker Engine | **Sec+:** Virtualization / **N+:** Network Isolation |

---

## 🚀 Key Accomplishments (Step-by-Step)
- [x] **Zero Port-Forwarding:** Implemented Tailscale to eliminate the need for open ports on the Xfinity Gateway, reducing the attack surface.
- [x] **Resource Optimization:** Configured LXC containers for low-overhead networking services, maintaining stability on mobile hardware.
- [x] **Safe Maintenance:** Developed a "Safe Eject" protocol for external SSD storage to maintain Proxmox filesystem integrity.
- [x] **DNS Management:** Configured conditional forwarding and upstream DNS settings to balance privacy and local resolution.

---

## 📡 Networking & Security Concepts Applied
As part of my **Net+** and **Sec+** studies, I am actively applying the following:
* **The CIA Triad:** Ensuring **Availability** through redundant service planning and **Confidentiality** via WireGuard encryption.
* **OSI Model Troubleshooting:** Diagnosing connectivity issues across Layer 3 (IP addressing) and Layer 4 (UDP/TCP ports).
* **Network Hardening:** Using "Invisible" VPN tunnels to prevent botnet discovery and brute-force attacks.

---

## 🧪 Future Testing Roadmap
- [ ] **Docker VM Deployment:** Moving standalone services into a dedicated Docker environment.
- [ ] **Media Storage (Jellyfin):** Testing hardware passthrough for a Samsung SSD.
- [ ] **SIEM Integration (Splunk):** Plans to ingest Pi-hole logs for real-time threat analysis.
- [ ] **pfSense Firewall:** Implementing a virtualized pfSense router to practice **VLAN Segmentation**.

---

### **Contact & Portfolio**
**Yinshaokie Solomon Vang** *Aspiring Cybersecurity & Network Professional*
https://www.linkedin.com/in/yinshaokievang/ | 
