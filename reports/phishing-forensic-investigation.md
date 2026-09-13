# Phishing Campaign Forensic Investigation

**MediSure Healthcare Network — simulated incident investigation**  
**Investigation:** 27–28 June 2026  
**Analyst:** Sarah Asemota

> Portfolio version of a controlled lab investigation. The scenario and identities are simulated; no real patient data is included.

## Executive Summary

This investigation analysed a targeted phishing campaign against a simulated healthcare organisation. The investigation correlated Splunk SIEM logs with email forensics and threat-intelligence sources including VirusTotal, AbuseIPDB and AlienVault OTX.

### Key findings
- Two malicious IPs were identified: `103.225.77.255` and `89.144.44.41`.
- Phishing infrastructure included `access-accsecurity.com`, `sign.in`, `thebandalisty.com` and `mondayfeeds.com`.
- Four users showed evidence of interaction with phishing infrastructure.
- Email authentication showed SPF failure, no DKIM signature and DMARC errors.
- `103.225.77.255` had 41 abuse reports across 17 sources.
- `access-accsecurity.com` was assessed as a DGA-generated lookalike domain.
- The simulated incident was assessed as **Critical** risk.

## Investigation Methodology

1. Analysed proxy, firewall and authentication logs in Splunk.
2. Correlated internal source IPs with phishing domains and destination IPs.
3. Reviewed email authentication indicators: SPF, DKIM and DMARC.
4. Enriched indicators using VirusTotal, AbuseIPDB and AlienVault OTX.
5. Reconstructed the incident timeline.
6. Assessed likelihood and potential impact of compromise.
7. Produced containment, remediation and longer-term security recommendations.

## Technical Findings

### Splunk correlation
Proxy analysis identified access to `access-accsecurity.com` and `sign.in` from internal addresses `10.1.5.23` and `10.1.5.45`.

Firewall analysis identified traffic involving `89.144.44.41` and `103.225.77.255`.

A geolocation query identified a failed authentication attempt associated with Russia.

Example queries used:

```spl
source="medisure_phishing_combined_logs.csv" (url_domain="access-accsecurity.com" OR url_domain="sign.in") | stats count by user, src_ip, url_domain
```

```spl
source="medisure_phishing_combined_logs.csv" log_type="firewall" (dest_ip="89.144.44.41" OR dest_ip="103.225.77.255") | stats count by src_ip, dest_ip
```

```spl
source="medisure_phishing_combined_logs.csv" log_type="auth" location="Russia" | stats count by user, result, location
```

### Email authentication
- **SPF:** Fail
- **DKIM:** None
- **DMARC:** PermError

These results indicated that the message was not successfully authenticated and supported the phishing assessment.

### Threat intelligence
`103.225.77.255` had a substantial abuse history involving web spam, email spam and spoofing. `89.144.44.41` had no AbuseIPDB reports but was associated through passive DNS with `mondayfeeds.com`, suggesting potentially newly deployed infrastructure.

AlienVault OTX classified `access-accsecurity.com` as DGA-generated with high confidence.

## Indicators of Compromise

| Type | Indicator | Assessment |
|---|---|---|
| IP | `103.225.77.255` | Malicious / persistent phishing infrastructure |
| IP | `89.144.44.41` | Suspicious / newly deployed infrastructure |
| Domain | `access-accsecurity.com` | Primary phishing / lookalike domain |
| Domain | `sign.in` | Credential-harvesting domain |
| Domain | `thebandalisty.com` | Secondary C2/phishing domain |
| Domain | `mondayfeeds.com` | Passive-DNS linked infrastructure |
| Email | `no-reply@access-accsecurity.com` | Phishing sender |
| Email | `solutionteamrecognized03@gmail.com` | Secondary campaign sender |
| File | `phishing_sample.eml` | Phishing sample |

## Risk Assessment

**Overall risk: Critical**

Potential impact included credential compromise, lateral movement, access to electronic health records, exposure of sensitive information, ransomware deployment and operational disruption.

## Recommended Response

### Immediate — 0–24 hours
- Force password resets for affected users.
- Enforce MFA.
- Terminate active sessions.
- Block identified domains and IPs.
- Increase monitoring of affected accounts.

### Short term — 1–7 days
- Perform forensic review for lateral movement.
- Isolate affected systems if compromise is confirmed.
- Review email gateway and archive data.
- Rotate privileged credentials.
- Review access to sensitive records.

### Long term — 1–3 months
- Strengthen SPF, DKIM and DMARC enforcement.
- Implement URL filtering and click-time validation.
- Deliver phishing-awareness training.
- Integrate threat-intelligence feeds.
- Run incident-response tabletop exercises.
- Implement UEBA and EDR for critical systems.

## Skills Demonstrated

- SOC investigation
- SIEM log analysis with Splunk
- Threat intelligence
- IOC enrichment
- Phishing analysis
- Email authentication analysis
- Incident timeline reconstruction
- Risk assessment
- Incident response recommendations
- MITRE ATT&CK-informed analysis

## Tools

Splunk Enterprise, VirusTotal, AbuseIPDB, AlienVault OTX and email-header analysis.

## Disclaimer

This is a simulated cybersecurity portfolio project conducted in a controlled environment. Indicators and identities are presented for educational purposes and should not be treated as evidence of a real-world compromise.
