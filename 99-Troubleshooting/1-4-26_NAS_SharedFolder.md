# 📂 Procedure: Adding New Shared Folders

Follow these steps to provision new storage areas on the NAS while maintaining **Access Control** and **Data Integrity**.

## 🛠️ Step 1: Logical Directory Creation
1. Navigate to **Storage > Shared Folders**.
2. Click **+ (Create)**.
3. Select the **Samsung T7** (EXT4) as the host file system.
4. Name the folder (e.g., `Documents`, `Backups`, or `Photos`).
5. **Apply Changes** via the yellow confirmation bar.

## 🔐 Step 2: Access Control List (ACL) & Privileges
*Note: We follow the **Principle of Least Privilege**—only grant access to specific users.*

1. Navigate to **Users > Users**.
2. Highlight the target user (e.g., `Raya`).
3. Select **Shared folder permissions**.
4. Grant **Read/Write** access to the newly created folder.
5. **Apply Changes**.

## 📡 Step 3: Network Service Broadcast (SMB)
1. Navigate to **Services > SMB/CIFS > Shares**.
2. Click **+ (Create)** and link the logical folder to the SMB service.
3. **Security Setting:** Ensure **Public** is set to **No** to enforce password authentication.
4. **Apply Changes**.

---

## 🧠 Security+ Concept: Authorization vs. Authentication
* **Authentication:** Handled by Tailscale and the SMB login (Who are you?).
* **Authorization:** Handled by OMV Privileges (What are you allowed to touch?).
* By separating these, even if a user is *authenticated* to the server, they are only *authorized* to see folders specifically assigned to them.
  
[Back to Home](../01-HomeLab_Journey/01-README.md)
