# 🛠️ Troubleshooting: iOS "Read-Only" & Permission Denied

**Issue:** User can view folders in the iOS Files app but cannot **Paste**, **Move**, or **Delete** files (the "Paste" option is missing or an error occurs).

## 🕵️ Root Cause: Apple SMB Implementation
Apple devices use specific SMB extensions (metadata) that standard Linux configurations may not broadcast by default. Without these, iOS may default to a "Read-Only" state for security.

## 🚀 Resolution: Enabling Apple Compatibility & Write Access

### **Step 1: Enable Apple 'Fruit' Extensions**
1. Navigate to **Services > SMB/CIFS > Shares**.
2. Edit the target share (e.g., `Movies` or `YSV`).
3. Toggle **Time Machine Support** to **ON**.
    * *Note: This enables the `vfs_fruit` module, which improves interoperability between Linux and Apple's APFS/SMB protocols.*
4. **Apply Changes** (Yellow Bar).

### **Step 2: Verify User Authorization**
1. Navigate to **Users > Users** and highlight the user account.
2. Select **Shared folder permissions**.
3. Ensure the folder is set to **Read/Write** (not just Read-only).
4. **Apply Changes**.

### **Step 3: Recursive ACL Reset (If needed)**
If the folder was created on a different system or drive, permissions may be inconsistent.
1. Navigate to **Storage > Shared Folders**.
2. Highlight the folder and click **ACL**.
3. Grant **Read/Write/Execute** to the user and select **Recursive**.
4. **Apply Changes**.

---

## 🧠 Security+ Concept: Authorization vs. Interoperability
* **Authorization:** Validating that the authenticated user has the "Write" bit set in the filesystem.
* **Interoperability:** Ensuring the **SMB Protocol** translates those Linux permissions into a format the **iOS Kernel** understands.
