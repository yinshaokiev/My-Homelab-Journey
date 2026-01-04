# 🛠️ Network Incident Report: Pi-hole Patch Management & Repository Reconfiguration

**Date:** December 31, 2025  
**Technician:** YSV  
**Objective:** Perform critical system and application updates for the Pi-hole LXC container while resolving Proxmox repository authentication errors.

---

## 🔍 Problem Identification
1. **Application Stagnation:** The Pi-hole dashboard reported outdated Core, Web Interface, and FTL components, requiring manual intervention.
2. **Command Recognition Error:** The system failed to recognize the `pihole` command globally, leading to `bash: command not found` errors.
3. **Repository Authentication Gap:** Proxmox host updates were failing with **Exit Code 100** due to unauthorized attempts to reach the Enterprise subscription servers.

---

## 🛠️ Troubleshooting Steps & Methodology

### Phase 1: Environment Setup
* **Action:** Accessed the Proxmox Node (`ysv`) via Shell and identified the Pi-hole container ID.
* **Action:** Remotely entered the container environment using the Proxmox container toolkit: `pct enter 100`.
* **Outcome:** Successfully established a terminal session within the container and verified connectivity.

### Phase 2: System-Level Troubleshooting
* **Action:** Attempted a combined update command: `apt update && apt update pihole -up`.
* **Result:** **FAILURE.** Received "Command line option 'p' not understood."
* **Theory:** Suspected a syntax conflict between the system package manager (`apt`) and the application-specific update script (`pihole -up`).
* **Correction:** Segmented the update process into two distinct administrative phases: System Patching and Application Updating.

### Phase 3: Binary Verification & Path Configuration
* **Action:** Attempted `pihole -up` standalone.
* **Result:** **FAILURE.** Received `bash: pihole: command not found`.
* **Action:** Performed a manual directory search to locate the binary.
* **Resolution:** Identified the absolute path at `/usr/local/bin/pihole`. Executed the update using the full path to bypass environment variable limitations.

### Phase 4: Proxmox Host Hardening
* **Action:** Navigated to `ysv > Repositories` in the Proxmox Web UI.
* **Action:** Disabled the restricted `pve-enterprise` suite.
* **Action:** Implemented the `No-Subscription` repository to allow for verified security patches.
* **Result:** Successfully cleared **Exit Code 100**; verified system database refresh.

---

## 🏁 Phase 5: Resolution
* **Resolution:** All Pi-hole components (Core, Web, FTL) successfully transitioned to the latest versions.
* **Final Verification:** Dashboard confirms **"Everything is up to date!"** and DNS sinkhole services are fully operational.
<img width="1033" height="437" alt="Screenshot 2025-12-31 170800" src="https://github.com/user-attachments/assets/34047037-34d9-48ef-8877-a378b21930fc" />



---
## 🔗 Navigation
* [⬅️ Back to Troubleshooting](../99-Troubleshooting/)
* [🏠 Back to Main Menu](../01-HomeLab_Journey/01-README.md)

