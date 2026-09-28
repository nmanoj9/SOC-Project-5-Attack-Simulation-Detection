# SOC Project 5 — Network-Traffic-Analysis-Attack-Detection


## Overview

This project demonstrates a hands-on cybersecurity investigation workflow combining network traffic analysis, controlled attack simulation, Windows security telemetry, and network-to-endpoint correlation.

The project was conducted in an isolated VirtualBox laboratory environment using Kali Linux and Windows.

## Objectives

- Analyze network traffic using Wireshark
- Investigate Windows security events
- Simulate controlled security activity in a laboratory environment
- Correlate network and endpoint telemetry
- Identify indicators relevant to security investigations
- Develop detection logic from observed activity
- Document findings using an analyst-focused investigation workflow
- Preserve sanitized evidence suitable for a cybersecurity portfolio

## Lab Environment

| Component | Details |
|---|---|
| Test System | Kali Linux |
| Target System | Windows |
| Lab Network | 192.168.56.0/24 |
| Network Analysis | Wireshark |
| Endpoint Telemetry | Windows Security Logs |
| SIEM | Splunk |
| Endpoint Monitoring | Sysmon |
| Virtualization | VirtualBox |

## Investigation Focus

The investigation covers controlled network-based security activity and the correlation of network traffic with Windows endpoint telemetry.

Key areas include:

- SMB network communication
- SMB2 authentication traffic
- NTLM authentication
- Windows Security Event ID 4625
- Source IP and source port correlation
- Account-level investigation
- Logon Type 3 analysis
- Authentication failure analysis
- Network-to-endpoint event correlation
- Detection logic development

## Investigation Workflow

The investigation follows a practical security analyst workflow:

1. Generate controlled security activity
2. Capture network telemetry
3. Review relevant endpoint telemetry
4. Identify investigation indicators
5. Correlate network and endpoint evidence
6. Analyze the observed activity
7. Develop detection logic
8. Assess the security significance
9. Document findings
10. Preserve supporting evidence

## Evidence Handling

Only sanitized evidence suitable for public viewing is included in this repository.

Raw packet captures and evidence containing authentication information are retained privately and are not published.

## Repository Structure

```text
.
├── Documentation
│   └── Investigation Documentation
├── Evidence
│   └── Sanitized Investigation Evidence
└── README.md
```
## Key Skills Demonstrated

- Wireshark
- Network Traffic Analysis
- Packet Analysis
- Windows Security Event Analysis
- SMB Investigation
- NTLM Authentication Analysis
- Network-to-Endpoint Correlation
- Security Event Correlation
- Detection Logic
- Incident Investigation
- Technical Documentation
- Evidence Handling

## MITRE ATT&CK

Relevant activity was mapped to:

**T1021.002 — SMB/Windows Admin Shares**

## Disclaimer

All security testing was performed in an isolated laboratory environment using systems and accounts created for testing purposes.
