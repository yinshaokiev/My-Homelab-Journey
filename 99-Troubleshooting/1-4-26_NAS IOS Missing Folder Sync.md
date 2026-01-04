# 🛠️ Troubleshooting: iOS "Missing Folder" Sync Issue

**Problem:** New SMB shares (e.g., `TVShows`, `YSV`) appear on Windows/Android but are invisible on the iPhone/iPad **Files** app even though the server connection is active.

## 🕵️ Root Cause: Session Persistence
The iOS Files app often caches the initial directory list during the first **Handshake**. If new shares are added to OpenMediaVault later, the iOS **Client Cache** may not refresh automatically, leading to a "frozen" view of the server.

## 🚀 Resolution: Force Session Reset
Follow these steps to force the iPhone to download the updated directory list from the NAS:

1.  **Terminate the Active Session:**
    * Open the **Files app** and go to the **Browse** tab.
    * Tap the **Ellipsis (...)** > **Edit**.
    * Tap the **Remove/Eject** icon next to the NAS IP (`xxx.xxx.xx.xxx`).
2.  **Purge App Cache:**
    * Swipe up from the bottom of your iPhone and **Force Close** the Files app by swiping it away.
3.  **Re-Authenticate:**
    * Re-open **Files** > **Connect to Server**.
    * Use `smb://xxx.xxx.xx.xxx` and the `Raya` credentials.
    * Verify that all shares now appear in the root directory.

---

## 🧠 Security+ Tip: Caching vs. Security
* **Why caching exists:** It reduces network traffic and saves battery by not re-downloading the folder list every time you open the app.
* **The Security Trade-off:** Caching can lead to **Stale Data**. If you delete a folder or change permissions, an iPhone might still show the old folder name for a few minutes, even if access is technically denied.

[Back to Home](./99-Troubleshooting.md)
