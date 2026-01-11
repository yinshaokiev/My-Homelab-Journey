# 🏠 My Homelab Journey
This respository is my step by step learning process for setting up My first homelab built with Proxmox to learn virtualization, networking, backups, and automation
12/17/25 I started to learn how to transform my laptop into a proxmox server.

### 🖥️ Hardware: The "Dragon" (Asus GL502)

| Component | Specification |
| :--- | :--- |
| **CPU** | 8 x Intel(R) Core(TM) i7-7700HQ @ 2.80GHz |
| **RAM** | 16GB DDR4 |
| **Storage** | 500GiB SSD |
| **GPU** | NVIDIA GTX 1060 Mobile (6GB VRAM) |
| **OS** | Proxmox VE (Virtual Environment) |

## 🛠️ Services I plan to run 
- [x] **Pi-hole** - Network-wide ad blocking.
- [x] **Remote Access** - Tailscale for remote access
- [ ] **Home Assistant** - (Planned when I buy a home) Smart home orchestration. Acts as a central brain that forces all different brands to work together on a single screen.
- [x] **NAS setup** - Network Attached Storage Lab with primary purpose data storage
- [x] **NAS Folder** - NAS folder set up for personal docs.
- [x] **Media/NAS** - NAS setup with Movies and TV folder.  Mapped network drives to personal PC
- [ ] **Jellyfin** - setup Jelly fin to view media
- [ ] **Security + Lab** - Kali??
- [ ] **Honey Pot** - Sec + practice
---
## 🔗 Navigation
* [⬅️ Back to Troubleshooting](../99-Troubleshooting/)


## 📝 Latest Breakthrough

- 12/20/25 - Completed the task of turning my old Asus laptop into a [Proxmox server.](./03-proxmox-setup.md)
- 12/20/25 - Learned about Pi Hole and starting first Pi Hole project. 
- 12/20/25  [x] **[Pi-hole](./04-pihole-setup.md)** - Network-wide ad blocking.
- 12/21/25 - [Networking Incident Response & Troubleshooting - Xfinity Gateway Recovery & Proxmox Restoration](../99-Troubleshooting/12-21-25_networking.md)
- 12/21/25 - Learned about tailscale because I wanted to know if I can access my homelab outside of my homenetwork. 
- 12/22/25  [x] **[Tailscale-VPN](./05-Tailscale-setup.md)** - VPN remote accesss.
- 12/23/25 - [Netwokring Incident Response & Troubleshooting - Tailscale VPN Implementation & Proxmox LXC Hardening](../99-Troubleshooting/12-23-25_tailscale-lxc-fix.md)
- 12/23/25 - Reading up on next lab potential labs Honey pot and NAS. Not sure which one to do next.
- 12/31/25 - Deployed Tailscale across distributed endpoints (Windows & iOS) to create a private 'Tailnet'. This allows for secure, identity-verified SSH and Web GUI management of the home lab without the use of traditional VPN gateways or port forwarding.
- 12/31/25 - Deployed updates to [Proxmox](../99-Troubleshooting/12-31-25_ProxmoxUpdate.md) and [Pi-hole](../99-Troubleshooting/12-31-25_PiHoleUpdate.md)
- 01/04/26 - Deployed [NAS](./06-NAS-setup.md) and Mapped it to personal PC
- 01/04/26 - Troubleshooting Mapping NAS to personal PC [NAS Troubleshooting](../99-Troubleshooting/1-4-26_NAS_Troubleshooting.md)
- 01/10/26 - researched markdown syntax
- 01/10/26 - Siemlessly transfer files from phone directly to my NAS into a folder [NAS Troubleshooting](../99-Troubleshooting/1-10-26_NAS-Troubleshooting.md)
- 01/11/26 - Completed [Kali lab set up](./07-KaliLab-setup.md)
- 01/11/26 - Ran a Kali Lab [Network Reconnaissance](../99-Troubleshooting/1-11-26_Kali-Lab-nmap.md)
