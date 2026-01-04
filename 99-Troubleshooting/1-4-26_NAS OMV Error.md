# 🛠️ Troubleshooting: OMV-Salt Deploy Samba Error
**Error:** `ValueError: source code string cannot contain null bytes` or `AliasedLoader object has no attribute...`.

**Cause:** Corruption in the SaltStack cache files, preventing the Samba service from applying new configuration changes.

**Resolution:**
1. Log into Proxmox Console as `root`.
2. Clear cache: `rm -rf /var/cache/salt/minion/files/base/*`.
3. Sync grains: `omv-salt stage run prepare`.
4. Apply Samba fix: `omv-salt deploy run samba`.
---
## 🔗 Navigation
* [⬅️ Back to Troubleshooting](../99-Troubleshooting/)
* [🏠 Back to Main Menu](../01-HomeLab_Journey/01-README.md)
