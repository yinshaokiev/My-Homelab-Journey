# 🛠️ Troubleshooting: OMV-Salt Deploy Samba Error
**Error:** `ValueError: source code string cannot contain null bytes` or `AliasedLoader object has no attribute...`.

**Cause:** Corruption in the SaltStack cache files, preventing the Samba service from applying new configuration changes.

**Resolution:**
1. Log into Proxmox Console as `root`.
2. Clear cache: `rm -rf /var/cache/salt/minion/files/base/*`.
3. Sync grains: `omv-salt stage run prepare`.
4. Apply Samba fix: `omv-salt deploy run samba`.
5. 
## ✅ Post-Fix Verification Checklist
- [x] OMV Dashboard shows SMB/CIFS service as "Running".
- [x] Yellow "Apply Changes" bar completes without Jinja2 errors.
- [x] iPhone Files app can successfully 'Paste' a test file to the YSV folder.
- [x] `df -h` command confirms disk usage is within normal limits (<90%).
<img width="2008" height="695" alt="image" src="https://github.com/user-attachments/assets/9ba8153c-9dba-4850-b796-08aaa7a3e719" />

---
## 🔗 Navigation
* [⬅️ Back to Troubleshooting](../99-Troubleshooting/)
* [🏠 Back to Main Menu](../01-HomeLab_Journey/01-README.md)
