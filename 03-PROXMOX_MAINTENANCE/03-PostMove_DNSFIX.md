# Homelab Log: Post-Move Re-commissioning & DNS Fix

## 📌 Overview
* **Date:** July 2026
* **Milestone:** Relocated Homelab to the new townhome & restored core network services.
* **Primary Server:** Asus GL502 ("The Dragon") — Intel Core i7-7700HQ / 16GB DDR4 / Proxmox VE
* **Gateway IP:** `10.0.0.1` (Xfinity Gateway)
* **Pi-hole IP:** `10.0.0.165` (Container 100)

---

## 🛠️ Event 1: Server Relocation & Network Verification
1. **Graceful Power Down:**
   * Stopped file-sharing connections and executed clean shutdown of NAS (Container 102).
   * Sequentially stopped Splunk SIEM, Kali Lab, Pi-hole, and Tailscale nodes prior to shutting down the main Proxmox hypervisor (`ysv`).
2. **Re-commissioning:**
   * Reconnected "The Dragon" to the new Xfinity Gateway via Ethernet.
   * Confirmed the local subnet remained `10.0.0.0/24`, allowing all static IP assignments to persist seamlessly without needing re-IPing.

---

## 🐛 Event 2: Pi-hole DNS Bypass & Resolution

### **The Issue**
After reconnecting devices to the home Wi-Fi, ads were no longer being blocked. Running `nslookup flurry.com 10.0.0.165` confirmed that the Pi-hole engine was healthy and responding, but local devices were bypassing it.

### **Root Cause**
The Xfinity Gateway automatically assigns Comcast’s upstream DNS servers via DHCP:
* **IPv4 DNS:** `75.75.75.75`, `75.75.76.76`
* **IPv6 DNS:** `2001:558:feed::1`, `2001:558:feed::2`

Because Apple/iOS devices aggressively prioritize IPv6 and secondary DNS entries, keeping these Comcast entries in the list alongside `10.0.0.165` caused client devices to leak DNS requests outside the Pi-hole.

### **The Fix (Manual Client Configuration)**
1. On client devices (iOS / Desktop), switched DNS configuration from **Automatic** to **Manual**.
2. **Deleted all default ISP IPv4 and IPv6 DNS entries** (`75.75.75.x` and `2001:558:feed::x`).
3. Set **`10.0.0.165`** as the single primary DNS server.

> **Note:** Alternative long-term fixes include disabling DHCP on the Xfinity Gateway and enabling Pi-hole's internal DHCP server to handle automatic network-wide DNS distribution.

---

## 🔮 Future Expansion Planning
* **Hardware Evaluation:** Researched secondary mini-PCs (HP ProDesk 600 G2 vs. Lenovo ThinkCentre M75s-1 SFF) to establish a dual-node Proxmox cluster.
* **Architecture Goal:**
  * **Low-Power Node (Micro PC):** Run 24/7 core services (Pi-hole, Tailscale, pfSense) to maintain uptime during main host maintenance.
  * **High-Power Node ("The Dragon"):** Retain heavy workloads, Splunk SIEM logs, and Jellyfin media transcoding (leveraging Quick Sync on Intel HD Graphics 630).
