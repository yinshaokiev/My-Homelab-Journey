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
  * Target Status: "The Splunk web interface is at http://siem-server:8000"
  
  ---
## On the Attacker Machine (Kali - VM 103):
* Access via SSH or Console.
* Check if the Forwarder is running:
```bash
sudo /opt/splunkforwarder/bin/splunk status
```
  * Target status : "splunkd is running"
---
⚔️ Phase 2: Attack Simulation (The Red Team)
Scenario: SSH Brute Force (Password Guessing) Objective: Generate "Failed Login" events to test SIEM ingestion.

1. Pre-Flight Check (Kali)
Ensure the SSH service is actually running so we can attack it.

Bash
sudo systemctl start ssh
2. Execute Attack
Run the following command to simulate a bad actor trying to guess a password.

Bash
ssh badguy@localhost
3. Generate Noise
Prompt: badguy@localhost's password:

Action: Type random characters (e.g., admin123, password, 123456) and hit Enter.

Repeat: Do this 3 to 5 times rapidly.

Stop: Press Ctrl + C to cancel the session.

🛡️ Phase 3: Detection & Defense (The Blue Team)
Objective: Confirm Splunk captured the attack and identify the source.

1. Access the Watchtower
Open Browser: http://10.0.0.34:8000

Log in to Splunk.

Click "Search & Reporting".

2. Run the Hunt Query
Set time range to "Last 15 Minutes" and paste this query:

Code snippet
index=main "Failed password"
3. Analyze Results
Look for the following fields in the log events:

user: badguy (The fake account we used)

src_ip: ::1 or 127.0.0.1 (Localhost, since we attacked ourselves)

process: sshd

🔧 Troubleshooting Cheat Sheet
Problem: "Connection Refused" when attacking.

Fix: The SSH server is off. Run: sudo systemctl start ssh

Problem: No logs appearing in Splunk.

Check 1 (The Agent): Is the forwarder running? sudo /opt/splunkforwarder/bin/splunk restart

Check 2 (The File): Does the log file exist? ls -l /var/log/auth.log (If missing: sudo systemctl start rsyslog)

Check 3 (The Config): Is the input configured? sudo /opt/splunkforwarder/bin/splunk list monitor

🛑 Phase 4: Shutdown
Kali VM: sudo poweroff

Splunk VM: sudo poweroff

Proxmox: Leave running or shut down via web interface.
