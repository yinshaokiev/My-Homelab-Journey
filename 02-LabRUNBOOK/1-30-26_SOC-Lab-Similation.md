# 🕹️ SOC Lab Runbook: Operations & Simulations

**Purpose:** This document outlines the startup, execution, and detection procedures for the Home SOC Lab. Use this checklist to practice threat hunting workflows.

---

## 🚀 Phase 1: Startup Sequence

### 1. Boot the Infrastructure (Proxmox)
1. Log into Proxmox VE.
2. **Start VM 104 (Splunk Server)**.
   * *Wait ~2 minutes for the OS to boot.*
3. **Start VM 103 (Kali Linux)**.

### 2. Verify Services
**On the Splunk Server (VM 104):**
* Access via SSH or Console.
* Check if Splunk is running:
  ```bash
  sudo /opt/splunk/bin/splunk status
  ```

  ---
