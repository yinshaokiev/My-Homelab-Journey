# NAS Troubleshooting: Recovering and Automating Missing Files

* This guide documents the process of locating "missing" files on the OpenMediaVault (OMV) NAS and resolving permission issues for network users.
* As well as siemless being able to transfer files direcltly from my phone to a specific folder in my NAS.

## 📋 Problem Description
Files sent to the NAS via Tailscale (Taildrop) were not appearing in the expected network share (`YSV`) and were returning "Access Denied" errors on Windows clients.

## 🛠️ Resolution Steps

### 1. Locate the Physical Storage Path
OpenMediaVault mounts data drives under `/srv/` rather than `/mnt/`. Use `lsblk` to identify the unique ID (UUID) of the storage drive:
```bash
lsblk -f
Storage Drive: sdb1
```
*Mountpoint: /srv/dev-disk-by-uuid-78d9e59b-55d8-4fba-9d4f-6c61285ed1c4

### 2. Create an Administrative Shortcut (Symlink)
To avoid typing long UUID paths, create a symbolic link in the home directory:
```bash

ln -s /srv/dev-disk-by-uuid-78d9e59b-55d8-4fba-9d4f-6c61285ed1c4/YSV/ ~/YSV_Shortcut
```
### 3. Automate Taildrop Arrivals
Redirect the Tailscale file landing zone directly to the storage drive to prevent the OS drive from filling up:

```bash
sudo rm -r /var/lib/tailscale/files
sudo ln -s /srv/dev-disk-by-uuid-78d9e59b-55d8-4fba-9d4f-6c61285ed1c4/YSV /var/lib/tailscale/files
```
### 4. Resolve "Access Denied" (Permissions)
New files often arrive with restrictive permissions. Grant recursive read/write/execute access to the entire share for network users:

```bash

sudo chmod -R 777 /srv/dev-disk-by-uuid-78d9e59b-55d8-4fba-9d4f-6c61285ed1c4/YSV
```
### 5. Verify File Existence
Use a recursive list command to confirm files are physically present in the user-specific Tailscale folders:

```bash

ls -R /var/lib/tailscale/files
```

# 🧠 Security+ Tip: Caching vs. Security
* Why caching exists: It reduces network traffic and saves battery by not re-downloading the folder list every time you open an app.

* The Security Trade-off: Caching can lead to Stale Data. If you change permissions, a client might still show the old folder name or "Empty" status for a few minutes.

---
## 🔗 Navigation
* [⬅️ Back to Troubleshooting](../99-Troubleshooting/)
* [🏠 Back to Main Menu](../01-HomeLab_Journey/01-README.md)
