# Network Incident Report: Tailscale VPN Implementation & Proxmox LXC Hardening

**Date:** December 23, 2025  
**Technician:** YSV   
**Objective:** Establish a secure, encrypted remote access tunnel to the home lab using Tailscale while troubleshooting LXC container permission constraints.

---

## 🔍 Problem Identification
1. **Remote Access Gap:** Proxmox dashboard and local services were restricted to the local management network.
2. **Permission Constraints:** The initial Tailscale installation failed because the Proxmox container (LXC) was restricted from creating a virtual network tunnel (`/dev/net/tun`) by default.
3. **Service initialization error: the minimal Ubuntu template lacked necessary dependencies for the installation scrript. 

## 🛠️ Troubleshooting Steps & Methodology

### Phase 1: Environment Setup
* **Action:** Created a new Ubuntu 22.04 LXC container as a dedicated VPN gateway.
* **Action:** Configured a static internal IP to ensure network persistence within the lab.
* **Outcome:** Container established, but installation script failed initially due to missing `curl` dependencies in the minimal OS template.

### Phase 2: Service-Level Troubleshooting
* **Action:** Updated package repositories and installed dependencies: `apt update && apt install curl -y`.
* **Action:** Attempted to initialize the service using `tailscale up`.
* **Result:** **FAILURE.** Received error: `failed to connect to local tailscaled; it doesn't appear to be running`.

* **Theory:** Suspected the background daemon was crashing because the container lacked "Nesting" permissions and access to the host's TUN device.

### Phase 3: Hardware Passthrough & Configuration
* **Action:** Enabled **Nesting** in Proxmox under Container > Options > Features.
* **Action:** Performed a manual "Device Passthrough" by editing the host configuration file (`/etc/pve/lxc/[ID].conf`) to grant the container access to required kernel drivers.
* **Configuration Added:**
  ```text
  lxc.cgroup2.devices.allow: c 10:200 rwm
  lxc.mount.entry: /dev/net/tun dev/net/tun none bind,create=file

## Phase 4: Resolution
* **Resolution: After implementing device passtrhough for /'dev/net/tun the services successfully initialized and generated an OAuth autehnication URL.**
* **Final Verificaiton.  Tailscale Admin Console confirming both the Proxmox node and mobile client are acitve on private 'Tailnet'.**
* 
  <img width="1170" height="761" alt="image" src="https://github.com/user-attachments/assets/61356d6b-b25f-43c7-b9d9-4a359bbaf2aa" />


[Back to Home](../01-HomeLab_Journey/01-README.md)
