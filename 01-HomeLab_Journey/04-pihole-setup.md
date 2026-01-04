# 🚫 Pi-hole Installation
**Status:** ✅ Active
**Installation Type:** LXC Container (Debian 12)

## ⚙️ Configuration Details
- **IP Address:** `10.x.x.xxx` (Private!)
- **Upstream DNS:** Cloudflare (1.1.1.1)

## 📝 Installation Steps
1. Created a new CT (Container) in Proxmox.
2. Ran the official install script: `curl -sSL https://install.pi-hole.net | bash`.
3. Tested configurations on my iphone first.  Checked websties like CNN and Speedtest.com and all ads where gone. 
4. Configured my router's DNS settings to point to this container's IP.

## ⚠️ Challenges Encountered
- **Issue:** Gravity (the blocklist) wouldn't update at first.
- **Fix:** Realized the container didn't have internet access; fixed the Gateway setting in Proxmox.

### 🔧 Container Technical Specifications
| Setting | Value |
| :--- | :--- |
| **Container ID** | 100 |
| **OS Template** | Debian 13 (trixie) |
| **CPU Cores** | 1 |
| **RAM** | 512 MiB |
| **Root Disk** | 2 GiB |
| **Unprivileged** | Yes |

<img width="513" height="286" alt="image" src="https://github.com/user-attachments/assets/191f0c2d-bc4c-43fb-abab-7811e299b75b" />

---
## 🔗 Navigation
* [🏠 Back to Main Menu](../01-HomeLab_Journey/01-README.md)

