# 🛠️ Troubleshooting Guide - VM 102 (NAS)

This guide provides quick fixes for common issues encountered during the operation of the OpenMediaVault server.

## 🚨 Issue: "Windows Cannot Access \\10.x.x.xxx"
**Symptoms:** Network error popup or "Permission Denied" when trying to open the mapped M: drive.

### **Solution 1: Reset Windows Credentials**
Windows may be attempting to log in with cached, incorrect credentials.
1. Open **Command Prompt** as Administrator.
2. Run: `net use * /delete` and confirm with `Y`.
3. Re-map the drive using the `Raya` user credentials.

### **Solution 2: Verify SMB Service State**
1. Log into OMV Web GUI > **Services** > **SMB/CIFS**.
2. Ensure the service is **Enabled** (Green) and the **Movies** share is listed under the "Shares" tab.

---

## 🔌 Issue: SSD Unplugged or Not Found
**Symptoms:** The "Movies" folder is empty or the drive shows as "Missing" in OMV.

### **Solution: Re-bind the USB Device**
1. Ensure the Samsung T7 is physically plugged into the Proxmox host.
2. In **Proxmox**, go to **VM 102** > **Hardware**.
3. If the USB device shows "Error" or is missing, remove the entry and click **Add** > **USB Device** again.
4. Select the **Samsung T7** by Vendor/Device ID to ensure persistent mapping.

---

## ⏳ Issue: VM Won't Shutdown/Reboot
**Symptoms:** Error "TASK ERROR: VM quit/powerdown failed - got timeout".

### **Solution: Forced Stop**
1. Right-click **102 (nas)** in Proxmox.
2. Select **Stop** (this performs a hard power-off).
3. Click **Start** to boot fresh. *Note: Data integrity is protected because the SSD uses the EXT4 journaling file system.*

---

## 📂 Issue: Shared Folder Permissions
**Symptoms:** You can see the folder but cannot add or delete files.

### **Solution: Check ACL Privileges**
1. Go to OMV > **Storage** > **Shared Folders**.
2. Highlight the folder and click **Privileges**.
3. Ensure user `Raya` has **Read/Write** checked.
4. **Important:** Always click the **Yellow Bar Checkmark** to apply changes.

---
## 🔗 Navigation
* [⬅️ Back to Troubleshooting](../99-Troubleshooting/)
* [🏠 Back to Main Menu](../01-HomeLab_Journey/01-README.md)

