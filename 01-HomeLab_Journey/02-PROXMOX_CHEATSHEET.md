# 🛠️ Proxmox CLI & Troubleshooting Cheat Sheet

### Service Management
* `systemctl status pveproxy` - Check if the web dashboard service is running.
* `systemctl restart pveproxy` - Restart the web interface if it's not loading.

### Container (LXC) Management
* `pct list` - List all containers and their status.
* `pct start 100` - Start the container with ID 100 (Pi-hole).
* `pct status 100` - Verify if the container is currently running.

### Networking Commands
* `ip a` - Display all network interfaces and MAC addresses.
* `ip route` - View the default gateway (should be 10.0.0.1 - for xfinity).
* `ifup vmbr0` / `ifdown vmbr0` - Refresh the virtual network bridge.

---
[Back to Home](../01-HomeLab_Journey/01-README.md)
