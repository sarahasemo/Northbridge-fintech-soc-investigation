# Threat Intelligence Assessment

**Target:** Clear Secure Infrastructure (clearme.com) — simulated OSINT assessment  
**Investigation date:** 6 March 2026  
**Analyst:** Sarah Asemota

> Portfolio version of an OSINT and reconnaissance exercise. The assessment is presented for educational purposes.

## Objective

Assess the external attack surface and potential exposure associated with the target domain using open-source intelligence and reconnaissance techniques.

## Tools Used

- Google Search / DuckDuckGo
- Kali Linux
- theHarvester
- Shodan
- VirusTotal
- Whois
- Have I Been Pwned
- Google Dorks
- MITRE ATT&CK

## Reconnaissance Findings

The assessment identified:

- 43 IP addresses
- 4 publicly discoverable email addresses
- 3 ASNs
- 504 hosts/subdomains
- 11 interesting URLs

No immediate evidence of exposed sensitive information was identified during the reconnaissance phase.

## Email Exposure

A corporate service email appeared in historical breach datasets. The finding indicates potential exposure of corporate identity or credential-related information, but an appearance in a breach database does **not** by itself prove compromise of the organisation.

**Risk assessment:** Moderate to High.

## Network Intelligence

Most identified infrastructure appeared to be associated with legitimate cloud and network providers such as Cloudflare and AWS.

One IP address, `76.76.21.164`, was associated with a file named `CertiUtil.exe`. Sandbox behaviour was mapped to several MITRE ATT&CK techniques, including command and scripting, registry modification, access-token manipulation, obfuscated files and virtualisation/sandbox evasion. The infrastructure itself was assessed as low risk based on the available evidence.

## Attack Surface Observations

The investigation identified a large subdomain footprint, including development and verification hosts. A large digital footprint increases the importance of continuous subdomain discovery, service ownership and decommissioning controls.

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---|---|---|
| Execution | Command and Scripting Interpreter | T1059 |
| Persistence | Modify Registry | T1112 |
| Privilege Escalation | Access Token Manipulation | T1134 |
| Defense Evasion | Obfuscated Files or Information | T1027 |
| Defense Evasion | Virtualization/Sandbox Evasion | T1497 |

## Recommendations

### Identity and email security
- Enforce MFA.
- Monitor credential-stuffing attempts.
- Strengthen phishing awareness.

### Attack-surface management
- Perform regular subdomain audits.
- Decommission unused services.
- Monitor newly discovered subdomains.

### Continuous monitoring
- Implement threat-intelligence monitoring.
- Use SIEM detections for suspicious activity.
- Monitor for leaked credentials through appropriate threat-intelligence sources.

## Conclusion

The assessment demonstrated a substantial external digital footprint but did not identify clear evidence of active malicious compromise. The main security concern is attack-surface complexity, particularly the number of hosts and cloud infrastructure components. Continuous external attack-surface monitoring, access controls and proactive vulnerability management are recommended.

## Skills Demonstrated

- OSINT reconnaissance
- External attack-surface discovery
- Threat intelligence
- Subdomain enumeration
- IP and ASN analysis
- IOC assessment
- MITRE ATT&CK mapping
- Risk-based security recommendations

## Disclaimer

This is a simulated cybersecurity portfolio project conducted for educational purposes. Findings should not be interpreted as a real-world compromise assessment.
