# 🌐 Tailscale VPN Installation
**Status:** ✅ Active
**Installation Type:** LXC Container (Ubuntu 22.04)

## ⚙️ Configuration Details
- **Tailnet IP Address:** `100.x.x.xxx` (Private Mesh Network)
- **Auth Method:** OAuth via OIDC (secure single sign-on)

## 📝 Installation Steps
1. Container Provisioning: Created a new Ubuntu 22.04 LXC in Proxmox.
2. Dependency Management: Updated repositories and installed `curl` via `apt update && apt install curl -y`.
3. Deployment: Executed the Tailscale installation script: `curl -fsSL https://tailscale.com/install.sh | sh`.
4. Provisioning: Initialized the service and authenticated the node using `tailscale up`.
5. Verification: Confirmed the tunnel was active by accessing the Proxmox GUI from a mobile device over cellular data.

## ⚠️ Challenges Encountered
- **Issue:** The Tailscale daemon (tailscaled) failed to start, reporting a missing TUN device.
- **Fix:** Enabled Nesting in Proxmox and manually edited the container configuration file (`/etc/pve/lxc/101.conf`) to allow device passthrough for `/dev/net/tun`.
- **Troubleshooting guide** [Netwokring Incident Response & Troubleshooting - Tailscale VPN Implementation & Proxmox LXC Hardening](../99-Troubleshooting/12-23-25_tailscale-lxc-fix.md)

### 🔧 Container Technical Specifications
| Setting | Value |
| :--- | :--- |
| **Container ID** | 101 |
| **OS Template** | Ubuntu 22.04 LTS |
| **CPU Cores** | 1 |
| **RAM** | 512 MiB |
| **Root Disk** | 8 GiB |
| **Unprivileged** | No (Privileged container required for kernel device passthrough) |

<img width="1261" height="803" alt="image" src="https://github.com/user-attachments/assets/9f817caf-75a4-4289-b908-d477d9cc8dce" />

## 🛡️ Security Impact
- **Zero Trust:** Implemented identity-based access rather than relying on a traditional perimeter firewall.
- **Attack Surface Reduction:** Successfully established remote management without exposing Port 8006 to the public internet.

---
## 🔗 Navigation
* [🏠 Back to Main Menu](../01-HomeLab_Journey/01-README.md)

