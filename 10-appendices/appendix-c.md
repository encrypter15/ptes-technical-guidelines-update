# Appendix C - Creating the 'Only Safe Checks (Web)' Policy

---
**Copyright Notice**: The copyright holders of PTES and PTES-G maintain their copyrights. This is an open-source project to update the Guidelines.  
**Author**: Encrypter15, email: encrypter15@gmail.com maintains and asserts no rights to the information contained.  
**Date**: 2025-04-09  
**License**: This project is released under the MIT License as an open-source update to the PTES Technical Guidelines.  
---

# Creating the 'Only Safe Checks (Web)' Policy in OpenVAS

This document outlines the steps to configure an "Only Safe Checks (Web)" policy in OpenVAS (Greenbone Community Edition, as of April 09, 2025). This policy ensures non-disruptive scans for web applications.

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
- Name: `Only Safe Checks (Web)`
- Base: Select `Full and Fast`
- Click **Create**.

### 4. Edit the Configuration
- Locate "Only Safe Checks (Web)" and click the **Edit** icon.

### 5. Enable Web-Related NVT Families
- In **NVT Families**, click **Edit**.
- Enable "Web Servers" and "Web Applications".
- Save changes.

### 6. Remove Unsafe Plugins
- In the **Plugins** tab, filter with:
  ```
  "Denial of Service" OR "Exploit" -safe
  ```
- Uncheck disruptive plugins (e.g., "HTTP Flood").
- Retain safe plugins (e.g., "CGI Scanning," "SQL Injection (Safe)").
- Clear the filter to verify only safe plugins remain.

### 7. Configure Safe Preferences
- In **Preferences**:
  - Safe Checks: `Yes`
  - Max Threads: `3`
  - Silent: `Yes`
- Click **Save**.

### 8. Add HTTP Credentials
- Go to **Configuration** > **Credentials** > **New Credential**.
- Type: "Username + Password"
- Name: e.g., "Web Admin"
- Username: e.g., `admin`
- Password: e.g., `P@ssw0rd`
- Save.
- Link to "Only Safe Checks (Web)" under **Credentials**.
- Test:
  ```bash
  curl -u admin:P@ssw0rd http://target.com
  ```

### 9. Define a Target
- **Configuration** > **Targets** > **New Target**
- Name: e.g., "Web Target"
- IP/URL: e.g., `http://target.com`
- Add credentials.
- Save.

### 10. Set Up a Scan Task
- **Scans** > **Tasks** > **New Task**
- Name: e.g., "Web Safe Scan 2025-04-09"
- Scan Config: `Only Safe Checks (Web)`
- Scan Targets: "Web Target"
- Save and click **Start**.

### 11. Review Results
- After scan: **Scans** > **Results**
- Filter: "Severity > 0"
- Ensure no disruptive tests appear.
- Export: **Export > XML**

## Verification

- Test: Run against a test web server.
- Outcome: Completes without disruption, focusing on web-safe checks.
- Logs:
  ```bash
  sudo tail -f /var/log/gvm/*
  ```

## Notes

- Duration: May take longer due to ~5,000 web-specific NVTs.
- Customization: Adjust plugins for your web environment.
```

