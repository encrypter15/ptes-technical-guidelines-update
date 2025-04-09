# Appendix B - Creating the 'Only Safe Checks' Policy

---
**Copyright Notice**: The copyright holders of PTES and PTES-G maintain their copyrights. This is an open-source project to update the Guidelines.  
**Author**: Encrypter15, email: encrypter15@gmail.com maintains and asserts no rights to the information contained.  
**Date**: 2025-04-09  
**License**: This project is released under the MIT License as an open-source update to the PTES Technical Guidelines.  
---



# Creating the 'Only Safe Checks' Policy in OpenVAS

This document outlines the steps to configure an "Only Safe Checks" policy in OpenVAS (Greenbone Community Edition, as of April 09, 2025). This policy ensures non-disruptive vulnerability scans, avoiding tests that could crash services or trigger denial-of-service conditions, ideal for production environments.

## Prerequisites

- **OpenVAS Installed**: Ensure OpenVAS is running (e.g., on Kali Linux).
  ```bash
  sudo apt install openvas -y
  sudo openvas-setup
  ```
- **Web Access**: Log into the Greenbone Security Assistant (GSA) at `https://localhost:9392` with admin credentials.
- **Updated Feeds**: Sync NVTs:
  ```bash
  sudo greenbone-nvt-sync
  ```

## Steps to Create the Policy

### 1. Access the GSA Interface
- Open your browser and navigate to `https://localhost:9392`.
- Log in (e.g., username: `admin`, password from setup).

### 2. Go to Scan Configurations
- Navigate to **Configuration** > **Scan Configs** in the top menu.

### 3. Create a New Configuration
- Click the **New Scan Config** icon (star or plus sign).
- **Name**: `Only Safe Checks`
- **Base**: Select `Full and Fast`
- Click **Create**.

### 4. Edit the Configuration
- Locate "Only Safe Checks" and click the **Edit** icon (wrench or pencil).

### 5. Enable NVT Families
- In **NVT Families**, click **Edit**.
- Check all relevant families (e.g., "Windows," "Web Servers," "Port Scanners").
- Save changes.

### 6. Remove Unsafe Plugins
- Go to the **Plugins** tab.
- Filter with:
  ```
  "Denial of Service" OR "Exploit" -safe
  ```
- Uncheck disruptive plugins (e.g., "HTTP DoS Test").
- Retain safe plugins (e.g., "Port Scanners," "Service Detection").
- Clear the filter to verify only safe plugins remain.

### 7. Configure Safe Preferences
- In **Preferences**:
  - **Safe Checks**: Set to `Yes`
  - **Max Threads**: Set to `5`
  - **Silent**: Set to `Yes`
- Click **Save**.

### 8. Optional: Add Credentials
- For authenticated scans:
  - Go to **Configuration** > **Credentials** > **New Credential**.
  - Type: "Username + Password"
  - Name: e.g., "Safe Scan Creds"
  - Username: e.g., `admin`
  - Password: e.g., `P@ssw0rd`
  - Save.
- Link to "Only Safe Checks" under **Credentials**.
- Test:
  ```bash
  net use \\target_ip\IPC$ /user:admin P@ssw0rd  # Windows
  ssh admin@target_ip                           # Linux
  ```

### 9. Define a Target
- **Configuration** > **Targets** > **New Target**
- Name: e.g., "Safe Network"
- IP Range: e.g., `192.168.1.0/24`
- Add credentials (if used).
- Save.

### 10. Set Up a Scan Task
- **Scans** > **Tasks** > **New Task**
- Name: e.g., "Safe Scan 2025-04-09"
- Scan Config: `Only Safe Checks`
- Scan Targets: "Safe Network"
- Save and click **Start**.

### 11. Review Results
- After the scan: **Scans** > **Results**
- Filter: "Severity > 0"
- Ensure no disruptive tests appear.
- Export: **Export > XML**

### 12. Optional: Restrict Access
- **Administration** > **Users**
- Edit a user, add: "Only Safe Checks Config = Yes"
- Save.

## Verification

- **Test**: Run against a test VM.
- **Outcome**: Completes without service disruption, focusing on safe checks.
- **Logs**: Check for issues:
  ```bash
  sudo tail -f /var/log/gvm/*
  ```

## Notes

- **Duration**: May take longer due to ~30,000-50,000 safe NVTs.
- **Customization**: Adjust families/plugins as needed (e.g., skip "Mac OS X").
```

