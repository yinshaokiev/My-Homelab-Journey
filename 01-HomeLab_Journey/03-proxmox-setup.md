# Proxmox Installation Notes
**Date:** 12/20/25

### Post-Install Steps:
- [x] Installed Proxmox VE 8.x on Asus GL502.
- [x] Install Pi Hole 
- [ ] Install Media Hub like Jellyfin
- [ ] Install Windows 11 VM for testing 

## 🛠️ Troubleshooting Log

### Issue: IP Address 
- **The problem:** while watching youtube tutorial Proxmox VE Installation Guide I noticed my IP address was the same. 
- **The Fix:** I found that I had to direclty connect the laptop to an Ethernet connection.
- **Reasoning:** Using Ethernet isn't just a suggestion; it’s practically a requirement for a stable Proxmox environment. Since your server is the "foundation" for all your other virtual machines, if the foundation is shaky, everything on top of it will crash.
- Ethernet is designed to handle multiple "MAC addresses" (identities) on one port. This allows your Proxmox host, your Pi-hole, and your Honeypot to all have their own unique IDs on the network simultaneously.
- Wi-Fi adapters are usually "one-to-one." They struggle to pass traffic for multiple virtual identities at once, which often causes the connection to drop or prevents your VMs from getting an IP address.

### Issue: "No Subscription" Error
- **The Problem:** Every time I log in, Proxmox shows a warning that I don't have a paid license.
- **The Fix:** Found a script to disable the nag. 
- **Command used:** `curl -fssL https://proxmox-scripts.com/no-nag | bash`
- I was not able to disable the nag 12/20/25.  I will have to do some more research as to why its not working. 

### Issue: Laptop Goes to Sleep When Lid Closed
- **The Problem:** As soon as I closed the laptop, the server went offline.
- **The Fix:** Had to edit the `logind.conf` file in Linux.
- **File Path:** `/etc/systemd/logind.conf`
- **Change:** Set `HandleLidSwitch=ignore`.
- **The Fix:** Found 


---
## 🔗 Navigation
* [🏠 Back to Main Menu](../01-HomeLab_Journey/01-README.md)
