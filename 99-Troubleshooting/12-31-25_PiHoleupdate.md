🔧 Maintenance & Troubleshooting: Pi-hole Update Log
As part of regular lab maintenance, I performed a full system and application update for the Pi-hole LXC container. This process served as a practical exercise in Patch Management and Linux Terminal troubleshooting.

Update Procedure
To ensure a stable update, I followed a professional "OS-First" sequence:

1. System Database Update: Refreshed the local package index.
apt update

2. OS Patching: Upgraded all underlying Linux system packages to ensure compatibility.
apt upgrade -y

3. Application Update: Successfully executed the Pi-hole core update script.
pihole -up 


<img width="1033" height="437" alt="Screenshot 2025-12-31 170800" src="https://github.com/user-attachments/assets/010ae576-6e46-4370-a353-c82dd8cad60d" />

Challenges & Resolutions
During this update, I encountered and resolved several common Linux administration hurdles:

Syntax & Scope Errors:

Issue: Initially attempted to update the Pi-hole application via the apt package manager (e.g., apt update pihole -up).

Resolution: Identified the distinction between System Updates (apt) and Application Updates (pihole -up). Adjusted workflow to treat them as independent steps.

Command PATH Issues:

Issue: Received a bash: pihole: command not found error despite the service running correctly.

Resolution: Diagnosed the issue as a directory mapping error. Resolved by identifying the absolute path (/usr/local/bin/pihole) to verify the binary's existence and health.

Proxmox Repository (Exit Code 100):

Issue: Encountered a task failure in the Proxmox UI when refreshing the package database.

Resolution: Identified that the server was attempting to reach the "Enterprise" repository without a subscription. Successfully reconfigured the host to the No-Subscription repository, allowing for verified security updates.

Outcome
Current Status: All Pi-hole components (Core, Web Interface, and FTL) are fully patched and operational.

Skills Applied: Linux CLI, Patch Management, Troubleshooting, and Repository Configuration.
