# Northbridge-fintech-soc-investigation
SOC investigation project analysing suspicious activities using Wazuh, pfSense, Wireshark, Nmap, Hydra and Ubuntu
# Northbridge Fintech – SOC Investigation Project

## Overview
This project simulates a real-world Security Operations Center (SOC) investigation
conducted to assess and improve the security posture of a fintech environment.

The engagement focused on identifying suspicious activities, validating alerts,
and recommending remediation actions using industry-standard tools.

## Objective
- Investigate network anomalies
- Identify insecure services and attack vectors
- Detect malicious activity using SIEM
- Recommend remediation and long-term improvements

## Environment
- Target: Ubuntu Server (192.168.1.101)
- Attacker: Kali Linux (192.168.1.102)
- Tools: Wazuh (SIEM), pfSense (Firewall/IDS), Wireshark, Nmap, Hydra, Nikto, Snort

## Methodology
1. Network reconnaissance and port scanning
2. Attack simulation (FTP, SSH, HTTP)
3. Network traffic capture and analysis
4. SIEM alert correlation and threat hunting
5. Risk assessment and remediation planning

## Key Findings
- FTP (Port 21) exposed credentials in plaintext
- SSH (Port 22) vulnerable to brute force and privilege escalation
- ARP storm detected via Wireshark
- Medium overall risk score due to insecure services

## Tools Used
- Nmap
- Hydra
- Ubuntu
- Wireshark
- pfSense
- Wazuh SIEM

## Outcome
Critical security gaps were identified and remediation steps proposed to
reduce the organization’s risk posture and prevent unauthorized access.

## Disclaimer
This project was conducted in a controlled lab environment.
All data has been sanitized.

