# Appendix E - NeXpose Default Templates

---
**Copyright Notice**: The copyright holders of PTES and PTES-G maintain their copyrights. This is an open-source project to update the Guidelines.  
**Author**: Encrypter15, email: encrypter15@gmail.com maintains and asserts no rights to the information contained.  
**License**: This project is released under the MIT License as an open-source update to the PTES Technical Guidelines.  
---

# NeXpose Default Templates

This document lists the default scan templates provided by NeXpose (Rapid7 InsightVM) as of April 09, 2025. These templates define the scope and depth of vulnerability scans, tailored to various use cases.

## Overview

NeXpose offers preconfigured scan templates to address different scanning needs, from broad network audits to specific compliance checks. Each template balances scan depth, speed, and safety.

## Default Templates

### 1. Denial of Service
- **Description**: Tests for denial-of-service vulnerabilities using both safe and unsafe checks.
- **Use Case**: Isolated test environments where service disruption is acceptable.

### 2. Discovery Scan
- **Description**: Identifies live hosts on the network without vulnerability or policy checks.
- **Use Case**: Initial network mapping with minimal impact.

### 3. Discovery Scan (Aggressive)
- **Description**: Similar to Discovery Scan but includes port scanning and OS fingerprinting for faster, broader detection.
- **Use Case**: High-speed networks needing detailed host discovery.

### 4. Exhaustive
- **Description**: Comprehensive scan of all ports and vulnerabilities using safe checks, including patch and application-layer audits.
- **Use Case**: Detailed assessments where time and resources are not constraints.

### 5. Full Audit
- **Description**: Thorough network audit with safe checks, covering vulnerabilities, patches, and application-layer audits on default ports.
- **Use Case**: General security audits without disruption.

### 6. HIPAA Compliance
- **Description**: Audits compliance with HIPAA Section 164.312 (Technical Safeguards) using safe checks.
- **Use Case**: Healthcare environments requiring HIPAA adherence.

### 7. Internet DMZ Audit
- **Description**: Scans external-facing assets in the DMZ with safe checks, focusing on network vulnerabilities.
- **Use Case**: Assessing edge devices and public-facing systems.

### 8. Linux RPMs
- **Description**: Checks RPM-based Linux systems for vulnerabilities using safe checks.
- **Use Case**: CentOS/RHEL environments needing package-specific scans.

### 9. Microsoft Hotfix
- **Description**: Verifies Windows patch levels by KB number using safe checks.
- **Use Case**: Windows environments ensuring hotfix compliance.

### 10. Payment Card Industry (PCI) Audit
- **Description**: Assesses PCI DSS compliance with safe checks and detailed reporting.
- **Use Case**: Businesses handling card transactions preparing for PCI audits.

### 11. Penetration Test
- **Description**: Combines vulnerability scanning with light exploitation using safe checks.
- **Use Case**: Simulating attacks to validate vulnerabilities.

### 12. Safe Network Audit
- **Description**: Broad network audit with safe checks, excluding exploitation or policy checks.
- **Use Case**: Production networks requiring non-disruptive scans.

### 13. Sarbanes-Oxley (SOX) Compliance
- **Description**: Checks financial system compliance with SOX using safe checks.
- **Use Case**: Organizations ensuring SOX-compliant data integrity.

### 14. SCADA Audit
- **Description**: Assesses industrial control systems with safe checks, avoiding disruption.
- **Use Case**: SCADA environments needing careful scanning.

### 15. Web Audit
- **Description**: Scans web servers and applications for HTTP vulnerabilities without DoS tests.
- **Use Case**: Identifying XSS, SQLi, and web misconfigurations.

## Notes

- **Safe Checks**: Most templates use safe checks to avoid service disruption unless specified (e.g., Denial of Service).
- **Customization**: Templates can be duplicated and modified via the Security Console under **Administration** > **Scan Templates**.
- **Execution**: Select templates when creating a scan task in **Scans** > **Tasks**.

