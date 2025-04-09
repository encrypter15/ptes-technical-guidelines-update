# 1 Tools Required

---
**Copyright Notice**: The copyright holders of PTES and PTES-G maintain their copyrights. This is an open-source project to update the Guidelines.  
**Author**: Encrypter15, email: encrypter15@gmail.com maintains and asserts no rights to the information contained.  
**Date**: 2025-04-09  
**License**: This project is released under the MIT License as an open-source update to the PTES Technical Guidelines.  
---


This section outlines the tools required for penetration testing, updated to best-of-breed options as of 2025-04-09, with instructions on how to use them. These selections reflect decades of evolution in IT and InfoSec, tailored for both beginners and experienced practitioners.

## 1.1 Operating Systems
### 1.1.1 MacOS X
- **Tool**: macOS Sequoia 15.x or later
- **Usage**: Install via the App Store or create a bootable USB with the command: `sudo /Applications/Install\ macOS\ Sequoia.app/Contents/Resources/createinstallmedia --volume /Volumes/USB`. Install Nmap via Homebrew with `brew install nmap`, then perform a basic network scan: `nmap -sP 192.168.1.0/24`.

### 1.1.2 VMware Workstation
- **Tool**: VMware Workstation 17 Pro
- **Usage**: Download from the VMware website and install. Create a virtual machine by selecting 'New Virtual Machine', choosing an ISO (e.g., Kali Linux), and configuring at least 4GB RAM and 2 CPU cores. Start the VM by clicking 'Power On'.
  #### 1.1.2.1 Linux
  - **Tool**: Kali Linux 2025.x
  - **Usage**: Download the ISO from kali.org, mount it in VMware, and follow the installation prompts. Update the system and tools with `sudo apt update && sudo apt full-upgrade -y`. Perform a network discovery scan with `nmap 192.168.1.0/24`.
  - **Tool**: Ubuntu 24.04 LTS
  - **Usage**: Install via ISO in VMware. Add security tools with `sudo apt install nmap wireshark metasploit-framework`. Scan ports using `nmap -sS 10.0.0.0/24`.
  #### 1.1.2.2 Windows XP/7 (Updated to Windows 11 Pro)
  - **Tool**: Windows 11 Pro
  - **Usage**: Install via ISO in VMware. Enable Hyper-V for nested virtualization with `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V`. Install WSL2 with `wsl --install`, then run Kali within WSL using `wsl -d kali-linux`.

## 1.2 Radio Frequency Tools
### 1.2.1 Frequency Counter
- **Tool**: Rigol DG1000Z
- **Usage**: Connect to an RF source using a BNC cable. Power on the device, select 'Counter' mode via the front panel, and read the frequency on the display. Log results to a PC via USB using Rigol Ultra Sigma software.

### 1.2.2 Frequency Scanner
- **Tool**: Uniden SDS200
- **Usage**: Power on the scanner, navigate the menu to set a frequency range (e.g., 2400-2500 MHz for Wi-Fi), and initiate a scan. Save detected frequencies to a favorites list for analysis.

### 1.2.3 Spectrum Analyzer
- **Tool**: Rohde & Schwarz FPC1500
- **Usage**: Connect an antenna, power on the device, set the frequency range (e.g., 2.4 GHz), and adjust the span (e.g., 100 MHz). Use the 'Peak Search' function to identify signals. Export data via USB.

### 1.2.4 802.11 USB Adapter
- **Tool**: Alfa Network AWUS036ACHM
- **Usage**: Plug into a Linux VM (e.g., Kali). Enable monitor mode with `sudo airmon-ng start wlan0`, then capture packets using `airodump-ng wlan0mon`.

### 1.2.5 External Antennas
- **Tool**: TP-Link TL-ANT2424B
- **Usage**: Attach to a compatible adapter (e.g., Alfa AWUS036ACHM) via an RP-SMA connector. Orient the antenna toward the target access point and measure signal strength with `airodump-ng`.

### 1.2.6 USB GPS
- **Tool**: Garmin GLO 2
- **Usage**: Connect via USB or Bluetooth to a laptop. Install GPS tools on Linux with `sudo apt install gpsd gpsd-clients`, then log coordinates with `cgps` during mobile testing.

## 1.3 Software
- **Tool**: Nmap 7.95
- **Usage**: Install on Linux with `sudo apt install nmap` or on Windows via the official installer. Perform a detailed network scan with `nmap -A 192.168.1.0/24`.
- **Tool**: Wireshark 4.x
- **Usage**: Install with `sudo apt install wireshark` on Linux or via the Windows installer. Capture packets on an interface (e.g., `wlan0`) and apply a filter (e.g., `http.request`) to analyze traffic.
- **Tool**: Metasploit Framework 6.x
- **Usage**: Install with `sudo apt install metasploit-framework`. Launch with `msfconsole`, search for exploits using `search cve-2025`, select one with `use exploit/...`, and set the target with `set RHOST target_ip`.
- **Tool**: Burp Suite Professional 2025.x
- **Usage**: Download from PortSwigger and launch with Java. Configure the browser proxy to 127.0.0.1:8080, intercept requests in the 'Proxy' tab, and initiate a scan with the 'Scanner' module.
- **Tool**: John the Ripper 1.9.x
- **Usage**: Install with `sudo apt install john`. Crack passwords from a hash file with `john hash_file.txt` after extracting hashes (e.g., using `hashcat`).
- **Tool**: Aircrack-ng 1.7
- **Usage**: Install with `sudo apt install aircrack-ng`. Capture a WPA handshake with `airodump-ng wlan0mon -c 6 --bssid AP_MAC -w capture`, then crack it with `aircrack-ng capture-01.cap -w wordlist.txt`.

