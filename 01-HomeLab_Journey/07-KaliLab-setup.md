# 🐉 Project Dragon: Kali Linux Lab Setup

This repository documents the deployment of a Kali Linux 2025.4 penetration testing lab on a **Proxmox VE (Type-1 Hypervisor)** environment.

## 💻 Host Hardware: Asus GL502 ("The Dragon")
- **CPU:** Intel(R) Core(TM) i7-7700HQ (8 Cores @ 2.80GHz)
- **RAM:** 16GB DDR4
- **Storage:** 500GiB SSD
- **Hypervisor:** Proxmox Virtual Environment 8.x

## 🛠️ VM Configuration (Kali-Lab)
To ensure optimal performance for security auditing and network scanning, the following resource baseline was established:

| Setting | Configuration | Reason |
| :--- | :--- | :--- |
| **VM ID** | 103 | Unique identifier in Node ysv |
| **CPU Cores** | 2 (Type: Host) | Pass-through of i7-7700HQ features |
| **RAM** | 4096 MiB | Smooth multi-tasking for GUI tools |
| **Storage** | 80 GiB | Room for wordlists (RockYou) and tools |
| **Network** | VirtIO (Bridge) | High-speed virtualized networking |
<img width="904" height="664" alt="image" src="https://github.com/user-attachments/assets/79f63030-1928-4c55-bbe6-590fd227289d" />

## 🛡️ Security & Integrity
- **Verification:** Verified ISO integrity using **SHA-256 Checksum** prior to upload.
- **Isolation:** Deployed as a virtualized guest to prevent lateral movement to the host system.
- **Provisioning:** Enabled **Discard/Trim** to maintain SSD health and efficient storage utilization.

## 🚀 Installation Steps
1. **ISO Upload:** Transferred `kali-linux-2025.4-installer-amd64.iso` to `local` storage.
2. **Resource Mapping:** Defined CPU, RAM, and Disk according to the baseline above.
3. **Execution:** Initialized via **Graphical Install** in the Proxmox Console.
4. **Snapshot:** (Pending) Post-install snapshot `Fresh_Install` to enable rapid revert to known-good-state.  

 <img width="2559" height="1098" alt="image" src="https://github.com/user-attachments/assets/3e1a2c7a-61aa-4855-8788-498fb7d47551" />
