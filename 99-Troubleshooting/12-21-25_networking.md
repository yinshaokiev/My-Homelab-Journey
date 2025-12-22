# Network Incident Report: Xfinity Gateway Recovery & Proxmox Restoration

**Date:** December 21, 2025  
**Technician:** YSV   
**Objective:** Restore network admin access and re-establish connectivity to a Proxmox virtualized home lab.

---

## 🔍 Problem Identification
1. **Administrative Lockout:** Lost credentials for the Xfinity Gateway (Router), preventing port management and DNS configuration.
2. **Service Interruption:** Following a factory reset of the gateway, the Proxmox VE dashboard (`10.0.0.xxx:xxxx`) and Pi-hole (`10.0.x.xxx`) became unreachable over the local network.

## 🛠️ Troubleshooting Steps & Methodology

### Phase 1: Gateway Recovery
* **Action:** Performed a hard factory reset of the Xfinity Gateway using the WPS button long-press (60 seconds).
* **Outcome:** Regained access via default credentials; re-configured SSID and Admin password.

### Phase 2: Layer 1 & 2 Verification
* **Action:** Verified physical link lights on the ASUS Proxmox host.
* **Result:** Blinking green LEDs confirmed active Ethernet connectivity (Physical Layer).
* **Action:** Checked the Proxmox network stack via CLI(command line interface).
* **Observation:** `ip route` confirmed the server was correctly pointed to the new gateway at `10.0.0.x`.

### Phase 3: Service-Level Troubleshooting
* **Action:** Restarted the Proxmox proxy service using `systemctl restart pveproxy`.
* **Result:** Command returned success (exit code 0), but the web UI remained unreachable.
* **Theory:** Suspected stale ARP tables or Xfinity "Advanced Security" port blocking.

### Phase 4: Resolution (The "Power Cycle" Method)
* **Action:** Performed a synchronized power cycle of the Gateway, Proxmox host, and Spare PC.
* **Result:** **SUCCESS.** Connectivity restored. The reboot forced a refresh of the router’s DHCP and ARP tables, allowing the devices to "see" each other on the `10.0.x.x/24` subnet.

## ✅ Final Configuration & Verification
* **Proxmox UI:** Accessible via `https://10.0.x.xxx:xxxx`.
* **Pi-hole:** Successfully manually started the container using `pct start 100`.
* **Persistence:** Configured **DHCP Reservations** in the gateway for both the Proxmox host and the Pi-hole container to prevent future IP drift.

---

## 🧠 Lessons Learned (Security+ Focus)
* **DHCP vs. Static:** While the server had a static IP, the router's lack of a matching **DHCP Reservation** caused a discovery conflict after the reset.
* **The "HTTPS" Trap:** Browsers often block local self-signed certificates (Port 8006). Documentation must include the "Advanced -> Proceed" step for future reference.
* **Troubleshooting Step 7:** Always document the solution. What seemed like a "broken server" was actually a "confused router."
