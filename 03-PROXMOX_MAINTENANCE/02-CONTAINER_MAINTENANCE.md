# 📦 LXC Container Maintenance Runbook

**Purpose:** Standard procedures for updating the application containers (Pi-hole, Tailscale, NAS).
**Frequency:** Once per month (Schedule it with your Proxmox Host update).

---

## 🛑 Pre-Flight: Safety First
Before updating *anything* critical like DNS (Pi-hole) or Remote Access (Tailscale), take a Snapshot!
1. Go to Proxmox Web UI.
2. Click the Container (e.g., **100 (pihole)**).
3. Click **Snapshots** -> **Take Snapshot**.
4. Name it `pre-update`.
   * *If the update breaks something, just click "Rollback" to fix it instantly.*

---

## 🥧 1. Pi-hole (CT 100)
*Pi-hole has two layers to update: the Linux OS underneath and the Pi-hole software itself.*

### Step 1: Update the OS
1. Open the **Console** for CT 100.
2. Run the standard Linux update:
   ```bash
   apt update && apt upgrade -y
   ```
Step 2: Update Pi-hole Software
Run the specific Pi-hole updater command:   
```bash
pihole -up
```
Verification:
* Go to your Pi-hole dashboard (`http://10.0.0.x/admin`).
* Check the footer. It should say "Pi-hole v5.x.x (Latest)".
---
## 🦎 2. Tailscale VPN (CT 101)
Tailscale is critical for remote access. Update carefully.

Step 1: Update the OS
* Open the Console for CT 101.
* Run the OS update:
```Bash
apt update && apt upgrade -y
```
Step 2: Update Tailscale Client
Tailscale has a built-in updater command (if installed via the official script):
```Bash
tailscale update
```
* If that command says "not found," the `apt upgrade` in Step 1 likely already handled it.
---
## 💾 3. NAS / File Server (CT 102)
This is likely a standard file server (Samba/NFS).

Step 1: Update the OS
* Open the Console for CT 102.
* Run the update:
```Bash
apt update && apt upgrade -y
```
Step 2: Maintenance Check (Optional)
* While you are here, check your disk space usage to ensure the drive isn't full:
```Bash
df -h
```
  * Look at the line mounted on `/` or `/mnt/data`. If it says 90%+, you might need to expand the disk in Proxmox.
---
## 🧹 Post-Maintenance Cleanup
Once you verify everything is working (Internet works, VPN connects, Files are accessible):
* Go back to Snapshots for each container.
* Delete the `pre-update` snapshot to save space.

