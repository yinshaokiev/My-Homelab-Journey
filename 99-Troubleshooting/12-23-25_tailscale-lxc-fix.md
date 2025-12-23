🛠️ Troubleshooting Guide: Tailscale on Proxmox LXC
Issue 1: Command Not Found (curl)
Symptoms: When running the installation script, the console returns: bash: curl: command not found.

Cause: Minimalist Linux templates (like Ubuntu/Debian) often exclude the curl utility to save space.

Resolution: Run the following commands to update the package repository and install the missing tool:
apt update
apt install curl -y

ssue 2: Tailscale Daemon Not Running
Symptoms: After installation, running tailscale up returns: failed to connect to local tailscaled; it doesn't appear to be running.

Cause: The background service (daemon) failed to start, usually due to a lack of permissions to create a network tunnel.

Resolution: 1. Enable Nesting: Ensure LXC > Options > Features > Nesting is checked. 2. Force Start: Manually trigger the service in the console:
systemctl enable tailscaled
systemctl start tailscaled

Issue 3: Permission Denied / TUN Device Missing
Symptoms: Tailscale fails to start even with Nesting enabled. The error log shows: failed to create TUN device.

Cause: Unprivileged or strictly sandboxed containers are blocked from creating the virtual network adapters required for VPNs.

Resolution (The "Guaranteed Fix"): Manually edit the container configuration file on the Proxmox Host Shell to allow device passthrough:

Open the config file (replace ID with your container ID, e.g., 101): nano /etc/pve/lxc/ID.conf

Add these lines to the bottom of the file:
lxc.cgroup2.devices.allow: c 10:200 rwm
lxc.mount.entry: /dev/net/tun dev/net/tun none bind,create=file

Restart the container for changes to take effect.

Key Cybersecurity Concepts Learned
Principle of Least Privilege: Understanding why Proxmox blocks hardware access by default to prevent a "container escape".

Service Management: Using systemctl to manage background processes.

Encapsulation: How VPNs use the TUN/TAP driver to wrap data in encrypted packets.
