# 🐲 Transforming "The Dragon" into a Proxmox Hypervisor

This guide documents the conversion of an **Asus GL502 Gaming Laptop** into a dedicated **Type-1 Hypervisor** using Proxmox VE. 

## 🛠️ Hardware Specifications
- **Model:** Asus GL502 ("The Dragon")
- **CPU:** Intel i7-7700HQ (4 Cores / 8 Threads)
- **RAM:** 16GB DDR4
- **Primary Storage:** 500GB SSD
- **Network:** Realtek Gigabit Ethernet + Intel Wireless

## ⚙️ Installation Process

### 1. BIOS Preparation (The "Handshake")
To allow Proxmox to control the hardware directly, the following BIOS settings were applied:
- **VT-x / Virtualization Technology:** Enabled (Required for running 64-bit VMs).
- **Secure Boot:** Disabled (Allows the Proxmox kernel to load).
- **SATA Mode:** AHCI (Standard for SSD performance).

### 2. Flash & Boot
- **Tool:** Used **Rufus** (or Etcher) to flash the Proxmox ISO to a USB drive.
- **Boot Key:** Tapped `Esc` or `F2` to enter the boot menu and selected the USB drive.

### 3. Installation Settings
| Setting | Selection | Reason |
| :--- | :--- | :--- |
| **Target Disk** | 500GB SSD | Primary system and VM storage. |
| **Hostname** | `ysv` | The unique name for this node in the network. |
| **IP Address** | Static IP | Ensures the server address doesn't change (Important for OMV/NAS). |
| **Filesystem** | ext4 (or ZFS) | Standard, reliable filesystem for a single-disk setup. |

## 🛡️ Post-Install Hardening
- **Web Interface:** Accessed the dashboard via `https://[IP-Address]:8006`.
- **Repository Setup:** Switched to the "No-Subscription" repository to receive community updates.
- **Tailscale Integration:** Installed Tailscale on the host to enable secure remote access from work/outside the home.

## 🧠 Security+ Concepts Applied
- **Type-1 Hypervisor:** Installed Proxmox directly on the hardware (Bare Metal) for maximum efficiency and security isolation.
- **Availability:** The laptop's built-in battery acts as a **UPS (Uninterruptible Power Supply)**, preventing data corruption during accidental power loss.
- **Remote Access (VPN):** Utilized Tailscale to implement a **Zero Trust** connection instead of dangerous Port Forwarding.

---
## 🔗 Navigation
* [🏠 Back to Main Menu](../01-HomeLab_Journey/01-README.md)
