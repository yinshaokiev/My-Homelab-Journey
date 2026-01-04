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

## Link Syntax
* `..` - This tells the computer to "step out" of the current folder
* `.` - This tells the computer to view the current file 
* `/` - THis means "look inside the directory I just stepped into".
* `Filename.md` - The name of the file you want to open
* `**name**` - This will Bold the text

---
## **Example Linking Down into a folder:**
* If you are editing your HomeLab Journey and want to link to the file inside the folder, use this syntax:
* ` [View Proxmox cheat sheet](./02-PROXMOX_CHEATSHEET.md)`
* `./` : Start in the current folder.
* `02-PROXMOX_CHEATSHEET.md` : Open the file within the folder.
---
## **Example Linking Up out of a folder:**
* If you are editing Troubleshooting and want to link to the files outside of the folder, use this syntax:
* `[View incident 12-21-25](../12-21-25_networking.md)`
* `../` : This tells the computer to "step out" or go up one level to the parent directory.
* `12-21-25_networking.md` : Opens the files sitting in that directory. 

---
## 🔗 Navigation
* [🏠 Back to Main Menu](../01-HomeLab_Journey/01-README.md)

