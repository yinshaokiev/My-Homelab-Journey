# 🛠️ Proxmox Host Maintenance Runbook

* **Purpose:** This document outlines the standard operating procedure (SOP) for patching and updating the Proxmox Virtual Environment (VE) hypervisor.
* **Frequency:** Recommended once per month or when critical security patches are released.

---

## 🚀 Phase 1: Pre-Update Health Check

Before applying updates to the core server, ensure the environment is stable.

### 1. Check Node Status
1. Log in to the Proxmox Web Interface (`https://10.0.0.x:xxx`).
2. Verify that CPU and RAM usage are normal.
3. Ensure no VMs are currently in a "locked" or "error" state.

### 2. Verify Backups (Optional but Recommended)
* If you have critical data, run a quick backup of your VMs (Kali/Splunk) before touching the host.

---

## ⚡ Phase 2: The Update Process

You can update Proxmox via the **Web GUI** (easier) or the **Shell** (faster/more reliable).

### Option A: The Web GUI Method
1. Click on your Node name (**ysv**) in the left menu.
2. Click **Updates** in the center menu.
3. Click the **Refresh** button at the top.
   * *Wait for "Task OK".*
4. Click the **Upgrade** button.
   * *This opens a popup terminal window.*
5. Type `Y` and hit **Enter** when asked to continue.
6. Wait for the process to finish (Look for "Your system is up-to-date").

### Option B: The Shell (CLI) Method
*Preferred for major updates.*

1. Click on your Node name (**ysv**) -> **Shell**.
2. Run the update command:
   ```bash
   apt update && apt dist-upgrade -y
   ```
   * Note: Always use `dist-upgrade` on Proxmox, never just `upgrade`, to ensure kernel dependencies are handled correctly.
  ---
  ## 🔄 Phase 3: Post-Update & Reboot
1. Check for Kernel Updates
Look at the output of the update. If you see lines mentioning `pve-kernel` or `linux-image`, a reboot is required to apply the changes.

2. Reboot the Hypervisor
* Warning: This will shut down ALL running VMs (Splunk, Kali, etc.).
* Ensure all VMs are stopped or ready to be paused.
* In the Shell, run:
```bash
reboot
```
3. Verify Version
Once the server comes back online:
* Log back into the Web Interface.
* Look at the top banner next to the Proxmox logo.
  * Example: `Proxmox VE 8.1.x`
* Ensure your VMs (Kali/Splunk) start up automatically (if "Start at boot" is enabled) or start them manually.
