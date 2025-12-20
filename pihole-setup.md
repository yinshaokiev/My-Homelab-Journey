# 🚫 Pi-hole Installation
**Status:** ✅ Active
**Installation Type:** LXC Container (Debian 12)

## ⚙️ Configuration Details
- **IP Address:** `10.0.0.xxx` (Private!)
- **Upstream DNS:** Cloudflare (1.1.1.1)

## 📝 Installation Steps
1. Created a new CT (Container) in Proxmox.
2. Ran the official install script: `curl -sSL https://install.pi-hole.net | bash`.
3. Tested configurations on my iphone first.  Checked websties like CNN and Speedtest.com and all ads where gone. 
4. Configured my router's DNS settings to point to this container's IP.

## ⚠️ Challenges Encountered
- **Issue:** Gravity (the blocklist) wouldn't update at first.
- **Fix:** Realized the container didn't have internet access; fixed the Gateway setting in Proxmox.
