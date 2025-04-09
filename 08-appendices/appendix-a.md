# Appendix A - Creating OpenVAS 'Only Safe Checks' Policy

---
**Copyright Notice**: The copyright holders of PTES and PTES-G maintain their copyrights. This is an open-source project to update the Guidelines.  
**Author**: Encrypter15, email: encrypter15@gmail.com maintains and asserts no rights to the information contained.  
**Date**: 2025-04-09  
**License**: This project is released under the MIT License as an open-source update to the PTES Technical Guidelines.  
---


# OpenVAS "Only Safe Checks" Policy Setup

![OpenVAS Logo](https://greenbone.github.io/docs/latest/_static/greenbone-community-edition.png)

Welcome to the repository for configuring an OpenVAS "Only Safe Checks" policy! This README provides detailed instructions to set up a non-disruptive vulnerability scanning policy using OpenVAS (Greenbone Community Edition). This configuration avoids tests that could crash services or trigger denial-of-service conditions, making it ideal for production environments.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration Steps](#configuration-steps)
- [Verification](#verification)
- [Notes](#notes)
- [Contributing](#contributing)
- [License](#license)

## Prerequisites

Before you begin, ensure the following:

- **OpenVAS Installed**: Running on a system like Kali Linux.
- **Web Interface Access**: Available at `https://localhost:9392` (or your server’s IP/port).
- **Updated Feeds**: Latest Network Vulnerability Tests (NVTs) synced.

## Installation

1. **Install OpenVAS** (if not already installed):
   ```bash
   sudo apt install openvas -y
   ```
2. **Configure OpenVAS**:
   ```bash
   sudo openvas-setup
   ```
   - Note the generated admin password.
3. **Sync NVT Feeds**:
   ```bash
   sudo greenbone-nvt-sync
   ```

## Configuration Steps

Follow these steps to create the "Only Safe Checks" policy:

### 1. Log into the Greenbone Security Assistant (GSA)
- Open your browser and go to `https://localhost:9392`.
- Log in with your admin credentials (e.g., `admin` and the setup password).

### 2. Navigate to Scan Configurations
- From the top menu: **Configuration** > **Scan Configs**.

### 3. Create a New Scan Configuration
- Click the **New Scan Config** icon (star or plus sign).
- **Name**: `Only Safe Checks`
- **Base**: Select `Full and Fast`
- Click **Create**.

### 4. Edit the Scan Configuration
- Find "Only Safe Checks" and click the **Edit** icon (wrench or pencil).

### 5. Configure NVT Families
- Go to **NVT Families**, click **Edit**.
- Enable all relevant families (e.g., "Windows," "Web Servers," "Port Scanners").
- Save changes.

### 6. Filter Out Unsafe Plugins
- In the **Plugins** tab:
  - Filter with:
    ```
    "Denial of Service" OR "Exploit" -safe
    ```
  - Uncheck disruptive plugins (e.g., "HTTP DoS Test").
  - Keep safe plugins like "Port Scanners" and "Service Detection".
- Clear the filter to confirm only safe plugins remain.

### 7. Set Safe Checks Preference
- In **Preferences**:
  - **Safe Checks**: `Yes`
  - **Max Threads**: `5` (low impact)
  - **Silent**: `Yes` (reduce noise)
- Save settings.

### 8. Optional: Add Credentials (Authenticated Scans)
- For deeper scans:
  - **Configuration** > **Credentials** > **New Credential**
  - Type: "Username + Password"
  - Name: e.g., "Windows Admin"
  - Username: e.g., `admin`
  - Password: e.g., `P@ssw0rd`
  - Save
- Link to "Only Safe Checks" under **Credentials**.
- Test:
  ```bash
  net use \\target_ip\IPC$ /user:admin P@ssw0rd  # Windows
  ssh admin@target_ip                           # Linux
  ```

### 9. Define a Target
- **Configuration** > **Targets** > **New Target**
- Name: e.g., "Safe Internal Network"
- IP Range: e.g., `192.168.1.0/24`
- Add credentials (if applicable).
- Save.

### 10. Create a Scan Task
- **Scans** > **Tasks** > **New Task**
- Name: e.g., "Safe Scan 2025-04-09"
- Scan Config: `Only Safe Checks`
- Scan Targets: "Safe Internal Network"
- Save and click **Start** (play button).

### 11. Review and Export Results
- After completion: **Scans** > **Results**
- Filter: "Severity > 0"
- Verify no disruptive tests ran.
- Export: **Export > XML**

### 12. Restrict Access (Optional)
- **Administration** > **Users**
- Edit a user, add rule: "Only Safe Checks Config = Yes"
- Save.

## Verification

- **Test Environment**: Scan a test VM to ensure no disruptions.
- **Expected Outcome**: Completes safely, focusing on port scanning and service detection.
- Check logs for errors:
  ```bash
  sudo tail -f /var/log/gvm/*
  ```

## Notes

- **Scan Time**: May take longer (~30,000-50,000 NVTs).
- **Customization**: Adjust NVT families for your needs (e.g., skip "Mac OS X" if irrelevant).
- **Documentation**: Save this README for team reference.

## Contributing

Found a bug or have a suggestion? Open an issue or submit a pull request! Contributions are welcome to enhance this policy setup.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```

