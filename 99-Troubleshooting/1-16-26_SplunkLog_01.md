## 🔧 Troubleshooting Log (The "Real World" Stuff)

### 🛑 Issue 1: "Connection Refused" on Web UI
* **Symptom:** Web interface (`http://10.0.0.34:8000`) refused to load after installation.
* **Root Cause:** The service was installed but the `splunkd` daemon was not running.
* **Troubleshooting Steps:**
    1. **Attempt 1 (Standard Start):** Ran `sudo /opt/splunk/bin/splunk start --accept-license`.
       * *Result:* Process stalled or failed to bind to port 8000.
    2. **Attempt 2 (Restart):** Ran `sudo /opt/splunk/bin/splunk restart`.
       * *Result:* Failed with error: `Running Splunk Enterprise as root is deprecated... use the --run-as-root option`.
    3. **Fix (Force Root Start):**
       ```bash
       sudo /opt/splunk/bin/splunk start --run-as-root
       ```
       * *Result:* Success. Message received: `The Splunk web interface is available at http://siem-server:8000`.

### 🛑 Issue 2: Indexing Paused (Disk Space Error)
* **Symptom:** Splunk stopped ingesting logs immediately after setup. No results found for `index=*`.
* **Error Message:**
  > `The index processor has paused data flow... Current free disk space ... has fallen to 4643MB, below the minimum of 5000MB.`
* **Context:** The default enterprise safety buffer (5GB) was too aggressive for this lightweight Lab VM (which only had ~4.6GB free).
* **Fix (Configuration Change):**
  1. Navigate to **Settings > Server settings > General settings**.
  2. Locate **"Pause indexing if free disk space (in MB) falls below"**.
  3. Changed value from `5000` to `500`.
  4. Saved and refreshed the browser.

### ✅ Verification & Analysis

To confirm the SIEM was fully operational, we performed a "smoke test" by searching for internal system logs.

**1. The "Show Everything" Search**
* **Command:** `index=*`
* **Time Range:** `All Time`
* **Result:** The search returned **15,823 events** immediately. This high volume confirms that the "Monitor" input is actively reading the historical contents of `/var/log` rather than just waiting for new events.

**2. Evidence of Live Logging**
We successfully located a specific administrative action in the logs, proving the system is recording user behavior in real-time.
* **Log Entry Found:**
    ```text
    COMMAND=/opt/splunk/bin/splunk start --run-as-root
    ```
* **Why this matters:** This specific log entry matches the exact command we executed to fix the "connection refused" error. Finding this entry closes the loop, proving that **Action (Terminal) → Log (Linux) → Ingestion (Splunk)** is functioning correctly.

**3. Field Parsing Confirmation**
Splunk successfully parsed the raw text into searchable fields (verified in the left sidebar):
* **`host = siem-server`**: Correctly identified the machine name.
* **`source = /var/log/auth.log`**: Correctly identified the file origin (Authentication Logs).
* **`sourcetype = auth`**: Correctly applied the "Linux Authentication" data model, allowing us to filter by user (e.g., `root` vs `admin_ysv`).

  ---
## 🔗 Navigation
* [⬅️ Back to Troubleshooting](../99-Troubleshooting/)
* [🏠 Back to Main Menu](../01-HomeLab_Journey/01-README.md)  
