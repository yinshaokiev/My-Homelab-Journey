# Home Media Server (NAS) - VM 102

Documentation for the deployment and hardening of a virtualized OpenMediaVault (OMV) NAS on Proxmox.

## 🖥️ System Specifications
* **Host:** Proxmox VE
* **VM ID:** 102
* **OS:** OpenMediaVault (Debian-based)
* **CPU:** 2 Cores (Balanced for background tasks and GUI stability)
* **RAM:** 2GB
* **Boot Disk:** 32GB VirtIO Block
* **Storage:** 1TB Samsung T7 SSD (USB Pass-through)
* * USB Pass-through: Verified via Proxmox Hardware ID mapping and OMV Disk Management.

## 🛡️ Security & Hardening Configuration
### 1. Access Control
* **Principle of Least Privilege:** Created a dedicated media user (`Raya`) for network sharing.
* **Separation of Duties:** Admin dashboard and root console use unique credentials separate from the media user.

### 2. Service Hardening
* **SMB Protocol:** Restricted to SMB2/SMB3 to prevent legacy vulnerabilities (like WannaCry/SMBv1).
* **Hostname:** Configured as `nas.local` for simplified internal name resolution.

### 3. Fault Tolerance & Availability
* **USB Hotplug:** Enabled in Proxmox to allow for accidental physical disconnection without VM failure.
* **Persistent Binding:** Mounted storage via UUID to ensure data integrity across reboots or port swaps.

## 🛠️ Installation Highlights
1. **Network:** Assigned static-like IP via DHCP reservation at `xx.x.x.xxx`.
2. **Updates:** Performed full patch management and kernel update immediately after install.
3. **Snapshots:** Created baseline snapshots at `Fresh_Install` and `Working_SMB_Share` for rapid recovery.

## 📂 Shared Folders
| Folder Name | Protocol | User Access | Permissions |
| :--- | :--- | :--- | :--- |
| Movies | SMB/CIFS | Raya | Read/Write |
| TVShows | SMB/CIFS | Raya | Read/Write |

* Run this in the NAS console to move Taildrop files to the SSD
tailscale file get /srv/dev-disk-by-uuid-YOUR-UUID-HERE/Movies/
---
## 🔗 Navigation
* [🏠 Back to Main Menu](../01-HomeLab_Journey/01-README.md)

