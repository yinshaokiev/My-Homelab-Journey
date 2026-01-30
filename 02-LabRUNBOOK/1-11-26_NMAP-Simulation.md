# 🕵️ SOC Lab Runbook: Network Mapping (Nmap)

**Purpose:** This document outlines the procedures for conducting network reconnaissance using Nmap and verifying detection in the SIEM.

---

## 🚀 Phase 1: Startup Sequence

### 1. Boot the Infrastructure
1. **Start VM 104 (Target):** The Ubuntu/Splunk Server (`10.0.0.34`).
2. **Start VM 103 (Attacker):** The Kali Linux Machine.

### 2. Verify Visibility
**On Kali Linux:**
* Ensure you can reach the target:
  ```bash
  ping -c 4 10.0.0.34
  ```
* Ensure the Splunk Forwarder is running ( to log your commands):
  ```bash
  sudo /opt/splunkforwarder/bin/splunk status
  ```
  ---
  ## ⚔️ Phase 2: Attack Simulation (Reconnaissance)
Objective: Scan the target server to identify open ports and services. Note: We use sudo for these commands. This gives Nmap raw socket privileges and ensures the command is logged to auth.log for Splunk to catch.

Scenario 1: The "Stealth" Syn Scan
This is the default scan that checks common ports without completing the TCP handshake.
```bash
sudo nmap -sS 10.0.0.34
```
Scenario 2: The "Noisy" Version Scan
This interrogates open ports to find out exactly what software version is running.
```bash
sudo nmap -sV 10.0.0.34
```
Scenario 3: The "Aggressive" OS Detection
This tries to guess the operating system by analyzing packet responses.
```bash
sudo nmap -O 10.0.0.34
```

---

## 🛡️ Phase 3: Detection & Defense (The Blue Team)
Objective: Confirm Splunk captured the execution of the reconnaissance tool.

1. Access the Watchtower
Open Browser: `http://10.0.0.34:8000`

Log in to Splunk -> Search & Reporting.

2. Run the Hunt Query
Since we are monitoring the Attacker's command usage via `auth.log`, we search for the command itself.

Primary Query:
```Code snippet
index=main "COMMAND=/*nmap"
```
* Why this works: Linux logs `sudo` commands with the field `COMMAND=`.

Broad Query (If the above fails):
```Code snippet
index=main "nmap"
```
3. Analyze Results
Expand the event log. You should see a clear audit trail:
* host: `kali-lab`
* user: `ysv` (or your username)
* command: `/usr/bin/nmap -sS 10.0.0.34`
* timestamp: Matching your scan time.

---
## 🔧 Troubleshooting
Problem: Scan says "Host seems down".
* Fix: The target might be blocking Ping. Try adding `-Pn` to force the scan: `sudo nmap -Pn 10.0.0.34`

Problem: Splunk sees the `sudo` command but not the arguments.
* Context: By default, `auth.log` captures the binary run.
* Fix: Verify you are running Nmap with `sudo`. Regular user commands are not typically logged to `auth.log` unless you configured shell history logging (bash history).
---

## 🛑 Phase 4: Shutdown
* Kali VM: sudo poweroff
* Splunk VM: sudo poweroff
