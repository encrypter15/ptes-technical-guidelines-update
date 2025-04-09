# Appendix D - Creating the 'Validation Scan' Policy

---
**Copyright Notice**: The copyright holders of PTES and PTES-G maintain their copyrights. This is an open-source project to update the Guidelines.  
**Author**: Encrypter15, email: encrypter15@gmail.com maintains and asserts no rights to the information contained.  
**Date**: 2025-04-09  
**License**: This project is released under the MIT License as an open-source update to the PTES Technical Guidelines.  
---

# Creating the 'Validation Scan' Policy in OpenVAS

This document outlines the steps to configure a "Validation Scan" policy in OpenVAS (Greenbone Community Edition, as of April 09, 2025). This policy targets specific vulnerabilities to validate remediation efforts.

## Prerequisites

- OpenVAS Installed: Ensure OpenVAS is running.
  ```bash
  sudo apt install openvas -y
  sudo openvas-setup
  ```
- Web Access: Log into the Greenbone Security Assistant at `https://localhost:9392`.
- Updated Feeds: Sync NVTs:
  ```bash
  sudo greenbone-nvt-sync
  ```

## Steps to Create the Policy

### 1. Access the GSA Interface
- Open `https://localhost:9392` and log in.

### 2. Go to Scan Configurations
- Navigate to **Configuration** > **Scan Configs**.

### 3. Create a New Configuration
- Click the **New Scan Config** icon.
- Name: `Validation Scan`
- Base: Select `Empty`
- Click **Create`.

### 4. Edit the Configuration
- Locate "Validation Scan" and click the **Edit** icon.

### 5. Select Specific NVTs
- In the **Plugins** tab:
  - Search for NVTs by CVE or name (e.g., `CVE-2025-1234 Check`).
  - Check only the boxes for remediated vulnerabilities (5-10 NVTs).
- Ensure only targeted tests are enabled.

### 6. Configure Preferences
- In **Preferences**:
  - Safe Checks: `No`
  - Max Threads: `10`
- Click **Save**.

### 7. Add Credentials
- Go to **Configuration** > **Credentials** > **New Credential**.
- Type: "Username + Password"
- Name: e.g., "Validation Creds"
- Username: e.g., `admin`
- Password: e.g., `P@ssw0rd`
- Save.
- Link to "Validation Scan" under **Credentials**.

### 8. Define a Target
- **Configuration** > **Targets** > **New Target**
- Name: e.g., "Validation Target"
- IP Range: e.g., `192.168.1.10`
- Add credentials.
- Save.

### 9. Set Up a Scan Task
- **Scans** > **Tasks** > **New Task**
- Name: e.g., "Validation Scan 2025-04-09"
- Scan Config: `Validation Scan`
- Scan Targets: "Validation Target"
- Save and click **Start**.

### 10. Review Results
- After scan: **Scans** > **Results**
- Filter: "Severity > 0"
- Verify targeted vulnerabilities are tested.
- Export: **Export > XML**

## Verification

- Test: Run against a remediated system.
- Outcome: Confirms fixes with precise, rapid scanning.
- Logs:
  ```bash
  sudo tail -f /var/log/gvm/*
  ```

## Notes

- Duration: Quick due to limited NVTs (5-10).
- Customization: Update NVTs as remediation progresses.
```



