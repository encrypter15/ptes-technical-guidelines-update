# 2 Intelligence Gathering

---
**Copyright Notice**: The copyright holders of PTES and PTES-G maintain their copyrights. This is an open-source project to update the Guidelines.  
**Author**: Encrypter15, email: encrypter15@gmail.com maintains and asserts no rights to the information contained.  
**Date**: 2025-04-09  
**License**: This project is released under the MIT License as an open-source update to the PTES Technical Guidelines.  
---


This section provides updated tools and instructions for intelligence gathering in penetration testing. Thorough reconnaissance is critical to understanding the target environment before proceeding.

## 2.1 OSINT
### 2.1.1 Corporate
- **Tool**: LinkedIn Sales Navigator 2025
- **Usage**: Log into the platform, search for a company (e.g., 'xAI'), apply filters for location and role, and export the resulting leads to a CSV file.
- **Tool**: ZoomInfo Enterprise
- **Usage**: Register an account, query a company name, and use the 'Advanced Search' feature to compile organizational details. Export data via the API with a command like `curl -X GET 'https://api.zoominfo.com/...'`.

### 2.1.2 Physical
#### 2.1.2.1 Locations
- **Tool**: Google Maps API 2025
- **Usage**: Obtain an API key from Google Cloud Console, then query locations with `curl -X GET 'https://maps.googleapis.com/maps/api/geocode/json?address=company_name&key=YOUR_API_KEY'` to retrieve geographic coordinates.
#### 2.1.2.2 Shared/Individual
- **Tool**: Zillow API
- **Usage**: Acquire an API key, query property data with `curl -X GET 'https://api.zillow.com/...'` to distinguish between shared and individual spaces.
#### 2.1.2.3 Owner
- **Tool**: LexisNexis 2025
- **Usage**: Access the service with a subscription, search property records by address, and download ownership documents in PDF format.
  ##### 2.1.2.3.1 Land/Tax Records
  - **Tool**: County Records Online (e.g., Accela API)
  - **Usage**: Access via a local government portal or use the API with `curl -X GET 'https://api.accela.com/...'`, search by parcel number, and retrieve tax records.

### 2.1.3 Datacenter Locations
#### 2.1.3.1 Time Zones
- **Tool**: TimeZoneDB
- **Usage**: Register for an API key, query time zones with `curl -X GET 'http://api.timezonedb.com/v2.1/get-time-zone?key=YOUR_KEY&lat=37.7749&lng=-122.4194'` to map datacenter locations.
#### 2.1.3.2 Offsite Gathering
- **Tool**: Shodan 2025
- **Usage**: Sign up for an account, search for organizational assets with `org:company_name` in the web interface or CLI (`shodan search org:company_name`), and analyze the resulting IP addresses.
#### 2.1.3.3 Product/Services
- **Tool**: Censys 2025
- **Usage**: Log into the platform, search for software services with `services.software:product_name`, and export host data to a CSV file.
#### 2.1.3.4 Company Dates
- **Tool**: Wayback Machine API
- **Usage**: Query historical snapshots with `curl -X GET 'http://archive.org/wayback/available?url=company.com'` to retrieve archived website data.
#### 2.1.3.5 Position Identification
- **Tool**: Hunter.io 2025
- **Usage**: Register an account, search for emails with `domain:company.com`, and verify them using `curl -X GET 'https://api.hunter.io/v2/email-verifier?email=user@company.com&api_key=YOUR_KEY'`.
#### 2.1.3.6 Organizational Chart
- **Tool**: OrgChartNow
- **Usage**: Import a CSV file from LinkedIn or ZoomInfo into the web interface, generate an organizational chart automatically, and export it as a PNG.
#### 2.1.3.7 Corporate Communications
  ##### 2.1.3.7.1 Marketing
  - **Tool**: Brandwatch 2025
  - **Usage**: Log into the platform, configure a query for company marketing campaigns, and analyze sentiment through dashboard reports.
  ##### 2.1.3.7.2 Lawsuits
  - **Tool**: PACER 2025
  - **Usage**: Register an account, search case dockets by company name, and download relevant PDFs (note: fees apply).
  ##### 2.1.3.7.3 Transactions
  - **Tool**: EDGAR Online
  - **Usage**: Access SEC filings at sec.gov, search by company ticker symbol, and retrieve transaction reports.
#### 2.1.3.8 Job Openings
- **Tool**: Indeed API 2025
- **Usage**: Obtain an API key, query job listings with `curl -X GET 'https://api.indeed.com/ads/apisearch?publisher=YOUR_ID&q=company_name'` to scrape relevant data.

### 2.1.4 Relationships
#### 2.1.4.1 Charity Affiliations
- **Tool**: GuideStar 2025
- **Usage**: Search for a company name in the GuideStar database and download reports on nonprofit affiliations.
#### 2.1.4.2 Network Providers
- **Tool**: BGPView 2025
- **Usage**: Visit bgpview.io, search by ASN or company name, and map network providers.
#### 2.1.4.3 Business Partners
- **Tool**: Crunchbase 2025
- **Usage**: Query a company profile and export partner data via the API with `curl -X GET 'https://api.crunchbase.com/v4/...'`.
#### 2.1.4.4 Competitors
- **Tool**: SimilarWeb 2025
- **Usage**: Enter a company domain in the web interface, analyze the 'Competitors' tab, and export traffic data.

## 2.2 Individuals
### 2.2.1 Social Networking Profile
- **Tool**: Pipl 2025
- **Usage**: Search by name or email in the Pipl web interface to retrieve linked social profiles.
### 2.2.2 Social Networking Websites
- **Tool**: Social Searcher
- **Usage**: Enter an individual’s name in the web interface, monitor real-time posts across platforms, and export results.
### 2.2.3 Cree.py
- **Tool**: Cree.py 2.x
- **Usage**: Install with `pip install creepy`, then run `creepy -u username` to scrape geolocation data from social media.

## 2.3 Internet Footprint
### 2.3.1 Email Addresses
#### 2.3.1.1 Maltego
- **Tool**: Maltego 2025
- **Usage**: Install the software, create a new graph, add a domain entity, and run the 'To Emails' transform to harvest email addresses.
#### 2.3.1.2 TheHarvester
- **Tool**: TheHarvester 4.x
- **Usage**: Install with `sudo apt install theharvester`, then run `theharvester -d company.com -b google -l 500` to gather emails.
#### 2.3.1.3 NetGlub
- **Tool**: NetGlub 2.x
- **Usage**: Install from source, launch the GUI, input a domain, and execute the email extraction module.
### 2.3.2 Usernames/Handles
- **Tool**: Namechk 2025
- **Usage**: Visit namechk.com, enter a username, and check its availability across multiple platforms.
### 2.3.3 Social Networks
#### 2.3.3.1 Newsgroups
- **Tool**: Google Groups API
- **Usage**: Query archived posts with `curl -X GET 'https://groups.google.com/...'`.
#### 2.3.3.2 Mailing Lists
- **Tool**: Mail-List.com
- **Usage**: Search mailing list archives by keyword and download relevant threads.
#### 2.3.3.3 Chat Rooms
- **Tool**: DiscordScraper (Custom)
- **Usage**: Use a bot token and run `python discord_scraper.py --token YOUR_TOKEN --channel CHANNEL_ID` to log chat activity.
#### 2.3.3.4 Forums Search
- **Tool**: Boardreader 2025
- **Usage**: Search by username or keyword in the web interface and export forum posts as a CSV file.
### 2.3.4 Personal Domain Names
- **Tool**: WhoisXML API
- **Usage**: Query ownership details with `curl -X GET 'https://www.whoisxmlapi.com/whoisserver/WhoisService?domainName=example.com&apiKey=YOUR_KEY'`.
### 2.3.5 Personal Activities
#### 2.3.5.1 Audio
- **Tool**: AudioScrape (Custom)
- **Usage**: Run `python audioscrape.py --url audio_url` to extract metadata from online audio files.
#### 2.3.5.2 Video
- **Tool**: VideoIntel (Custom)
- **Usage**: Run `python videointel.py --url video_url` to analyze video metadata.
### 2.3.6 Archived Information
- **Tool**: Archive.today
- **Usage**: Submit a URL via the web interface to retrieve cached pages for analysis.
### 2.3.7 Electronic Data
#### 2.3.7.1 Document Leakage
- **Tool**: FOCA 2025
- **Usage**: Install on Windows, input a domain, scan for documents, and extract metadata.
#### 2.3.7.2 Metadata Leakage
  ##### 2.3.7.2.1 FOCA (Windows)
  - **Tool**: FOCA 2025
  - **Usage**: Load a document in the GUI, select 'Extract Metadata', and review the results.
  ##### 2.3.7.2.2 Foundstone SiteDigger (Windows)
  - **Tool**: SiteDigger 2.x
  - **Usage**: Install on Windows, enter a domain, run a Google dork scan, and export metadata findings.
  ##### 2.3.7.2.3 Metagoofil (Linux/Windows)
  - **Tool**: Metagoofil 3.x
  - **Usage**: Run `metagoofil -d company.com -t doc,pdf -l 200 -o output` to analyze metadata in output files.
  ##### 2.3.7.2.4 Exif Reader (Windows)
  - **Tool**: ExifTool GUI 2025
  - **Usage**: Install on Windows, drag an image into the GUI, and view EXIF data.
  ##### 2.3.7.2.5 ExifTool (Windows/OS X)
  - **Tool**: ExifTool 12.x
  - **Usage**: Run `exiftool image.jpg` to extract all metadata.
  ##### 2.3.7.2.6 Image Search
  - **Tool**: TinEye 2025
  - **Usage**: Upload an image to tineye.com and review reverse search results for its origin.

## 2.4 Covert Gathering
### 2.4.1 On-location Gathering
#### 2.4.1.1 Adjacent Facilities
- **Tool**: Google Earth Pro 2025
- **Usage**: Install the software, search for the target address, and use the 'Measure' tool to map adjacent facilities.
#### 2.4.1.2 Physical Security Inspections
  ##### 2.4.1.2.1 Security Guards
  - **Tool**: Bushnell Fusion X Binoculars
  - **Usage**: Use the binoculars to observe guard patterns from a distance and manually note schedules.
  ##### 2.4.1.2.2 Badge Usage
  - **Tool**: RFIDler
  - **Usage**: Connect to a PC, execute `rfidler.py`, and scan badges at close range to read RFID data.
  ##### 2.4.1.2.3 Locking Devices
  - **Tool**: LockPick Extreme
  - **Usage**: Use a tension wrench and pick to bypass locks, practicing on dummy locks beforehand.
  ##### 2.4.1.2.4 Intrusion Detection Systems (IDS)/Alarms
  - **Tool**: Flipper Zero
  - **Usage**: Flash the firmware, use the 'Infrared' or 'RF' module to test IDS signals.
  ##### 2.4.1.2.5 Security Lighting
  - **Tool**: FLIR ONE Pro Thermal Camera
  - **Usage**: Attach to a smartphone, scan the area to identify light coverage and blind spots.
  ##### 2.4.1.2.6 Surveillance/CCTV Systems
  - **Tool**: CCTV Analyzer (Custom)
  - **Usage**: Run `python cctv_analyzer.py --freq 2400` with a HackRF device to detect CCTV signals.
  ##### 2.4.1.2.7 Access Control Devices
  - **Tool**: Proxmark3
  - **Usage**: Launch with `pm3` and use `hf mf dump` to clone Mifare cards.
  ##### 2.4.1.2.8 Environmental Design
  - **Tool**: SketchUp 2025
  - **Usage**: Import site photos into the software and model the layout in 3D to identify vulnerabilities.
#### 2.4.1.3 Employee Behavior
- **Tool**: Social Engineering Toolkit (SET) 2025
- **Usage**: Run `setoolkit`, select the 'Phishing' option, craft an email, and monitor responses.
#### 2.4.1.4 Dumpster Diving
- **Tool**: Fujitsu ScanSnap iX1600
- **Usage**: Collect physical documents, scan them with ScanSnap (auto-OCR enabled), and review the digital copies.
#### 2.4.1.5 RF/Wireless Frequency Scanning
- **Tool**: HackRF One
- **Usage**: Connect to a PC, launch `gnuradio-companion`, and create a flowgraph to scan RF bands.

### 2.4.2 Frequency Usage
- **Tool**: SDR# 2025
- **Usage**: Install the software, connect a HackRF device, tune to a target frequency (e.g., 2.4 GHz), and log signals.

### 2.4.3 Equipment Identification
#### 2.4.3.1 Airmon-ng
- **Tool**: Airmon-ng 1.7
- **Usage**: Run `sudo airmon-ng start wlan0` to enable monitor mode on a Wi-Fi adapter.
#### 2.4.3.2 Airodump-ng
- **Tool**: Airodump-ng 1.7
- **Usage**: Run `airodump-ng wlan0mon -c 6 --bssid AP_MAC` to capture access point traffic.
#### 2.4.3.3 Kismet-Newcore
- **Tool**: Kismet 2025.x
- **Usage**: Install with `sudo apt install kismet`, then run `kismet -c wlan0` to detect networks.
#### 2.4.3.4 inSSIDer
- **Tool**: inSSIDer 6.x
- **Usage**: Install on Windows, launch the software, select an adapter, and view Wi-Fi signal strength.

## 2.5 External Footprinting
### 2.5.1 Identifying IP Ranges
#### 2.5.1.1 WHOIS Lookup
- **Tool**: WhoisXML API
- **Usage**: Query IP ranges with `curl -X GET 'https://www.whoisxmlapi.com/whoisserver/WhoisService?domainName=domain.com&apiKey=YOUR_KEY'`.
#### 2.5.1.2 BGP Looking Glasses
- **Tool**: BGPView 2025
- **Usage**: Visit bgpview.io, enter an ASN, and view route tables.

### 2.5.2 Active Reconnaissance
- **Tool**: Nmap 7.95
- **Usage**: Run `nmap -sS -p- 192.168.1.0/24` for a stealth TCP scan.

### 2.5.3 Passive Reconnaissance
- **Tool**: PassiveTotal 2025
- **Usage**: Log into the platform, search a domain, and review passive DNS data.

### 2.5.4 Active Footprinting
#### 2.5.4.1 Zone Transfers
  ##### 2.5.4.1.1 Host
  - **Tool**: Host 2.x
  - **Usage**: Run `host -t AXFR domain.com ns1.domain.com` to attempt a zone transfer.
  ##### 2.5.4.1.2 Dig
  - **Tool**: Dig 9.x
  - **Usage**: Run `dig @ns1.domain.com domain.com AXFR` to retrieve DNS zone data.
#### 2.5.4.2 Reverse DNS
- **Tool**: dnsrecon 2025
- **Usage**: Run `dnsrecon -r 192.168.1.0/24` to enumerate reverse DNS entries.
#### 2.5.4.3 DNS Bruting
  ##### 2.5.4.3.1 Fierce2 (Linux)
  - **Tool**: Fierce 2.5
  - **Usage**: Run `fierce -dns domain.com` to brute-force subdomains.
  ##### 2.5.4.3.2 DNSEnum (Linux)
  - **Tool**: DNSEnum 6.x
  - **Usage**: Run `dnsenum domain.com` for DNS enumeration.
  ##### 2.5.4.3.3 Dnsdict6 (Linux)
  - **Tool**: Dnsdict6 2.x
  - **Usage**: Run `dnsdict6 -d domain.com` for IPv6 DNS brute-forcing.
#### 2.5.4.4 Port Scanning
  ##### 2.5.4.4.1 Nmap (Windows/Linux)
  - **Tool**: Nmap 7.95
  - **Usage**: Run `nmap -p 1-65535 -T4 target_ip` for a full port scan.
#### 2.5.4.5 SNMP Sweeps
  ##### 2.5.4.5.1 SNMPEnum (Linux)
  - **Tool**: SNMPEnum 2.x
  - **Usage**: Run `perl snmpenum.pl target_ip public windows.txt` to enumerate SNMP data.
#### 2.5.4.6 SMTP Bounce Back
- **Tool**: SMTPing (Custom)
- **Usage**: Run `python smtping.py --target mail.domain.com` to test SMTP responses.
#### 2.5.4.7 Banner Grabbing
  ##### 2.5.4.7.1 HTTP
  - **Tool**: WhatWeb 2025
  - **Usage**: Run `whatweb http://target.com` to grab HTTP banners.

## 2.6 Internal Footprinting
### 2.6.1 Active Footprinting
#### 2.6.1.1 Ping Sweeps
  ##### 2.6.1.1.1 Nmap (Windows/Linux)
  - **Tool**: Nmap 7.95
  - **Usage**: Run `nmap -sn 192.168.1.0/24` for internal host discovery.
  ##### 2.6.1.1.2 Alive6 (Linux)
  - **Tool**: Alive6 2.x
  - **Usage**: Run `alive6 eth0` to detect IPv6 hosts.
#### 2.6.1.2 Port Scanning
  ##### 2.6.1.2.1 Nmap (Windows/Linux)
  - **Tool**: Nmap 7.95
  - **Usage**: Run `nmap -sU -p 1-1000 192.168.1.10` for UDP scanning.
#### 2.6.1.3 SNMP Sweeps
  ##### 2.6.1.3.1 SNMPEnum (Linux)
  - **Tool**: SNMPEnum 2.x
  - **Usage**: Run `perl snmpenum.pl 192.168.1.10 public linux.txt` to enumerate SNMP data.
#### 2.6.1.4 Metasploit
- **Tool**: Metasploit Framework 6.x
- **Usage**: Launch with `msfconsole`, use the module `auxiliary/scanner/snmp/snmp_enum`, set `RHOSTS 192.168.1.0/24`, and execute with `run`.
#### 2.6.1.5 Zone Transfers
  ##### 2.6.1.5.1 Host
  - **Tool**: Host 2.x
  - **Usage**: Run `host -t AXFR internal.domain.com ns.internal.domain.com` to attempt a zone transfer.
  ##### 2.6.1.5.2 Dig
  - **Tool**: Dig 9.x
  - **Usage**: Run `dig @ns.internal.domain.com internal.domain.com AXFR` to retrieve DNS zone data.
#### 2.6.1.6 SMTP Bounce Back
- **Tool**: SMTPing (Custom)
- **Usage**: Run `python smtping.py --target mail.internal.domain.com` to test SMTP responses.
#### 2.6.1.7 Reverse DNS
- **Tool**: dnsrecon 2025
- **Usage**: Run `dnsrecon -r 192.168.1.0/24` to enumerate reverse DNS entries.
#### 2.6.1.8 Banner Grabbing
  ##### 2.6.1.8.1 HTTP
  - **Tool**: WhatWeb 2025
  - **Usage**: Run `whatweb http://192.168.1.10` to grab HTTP banners.
  ##### 2.6.1.8.2 httprint
  - **Tool**: httprint 2.x
  - **Usage**: Run `httprint -h 192.168.1.10 -s signatures.txt` to fingerprint HTTP servers.
#### 2.6.1.9 VoIP Mapping
  ##### 2.6.1.9.1 Extensions
  - **Tool**: SIPVicious 2025
  - **Usage**: Run `svmap 192.168.1.0/24` to map SIP devices.
  ##### 2.6.1.9.2 Svwar
  - **Tool**: Svwar 2.x
  - **Usage**: Run `svwar -e 100-999 192.168.1.10` to enumerate VoIP extensions.
  ##### 2.6.1.9.3 enumIAX
  - **Tool**: enumIAX 2.x
  - **Usage**: Run `enumiax -r 192.168.1.10` to enumerate IAX2 protocol devices.
#### 2.6.1.10 Passive Reconnaissance
  ##### 2.6.1.10.1 Packet Sniffing
  - **Tool**: Wireshark 4.x
  - **Usage**: Launch the software, select an interface (e.g., `eth0`), apply a filter (e.g., `ip.addr == 192.168.1.10`), and analyze captured packets.

