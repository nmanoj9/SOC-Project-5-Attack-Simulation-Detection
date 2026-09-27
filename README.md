# SOC Project 5 — Attack Simulation & Detection

## Overview

This project demonstrates a hands-on SOC investigation workflow combining network traffic analysis, Windows security telemetry, attack simulation, and evidence-based incident investigation.

The project was conducted in an isolated VirtualBox lab environment using Kali Linux and Windows.

## Project Objectives

- Analyze network traffic using Wireshark
- Investigate Windows security events
- Simulate controlled security events in a lab environment
- Correlate network and endpoint telemetry
- Build detection logic from observed activity
- Document investigations using a SOC analyst workflow
- Produce sanitized evidence suitable for a cybersecurity portfolio

## Lab Environment

| Component | Details |
|---|---|
| Attacker/Test System | Kali Linux |
| Target System | Windows |
| Lab Network | 192.168.56.0/24 |
| Network Analysis | Wireshark |
| Endpoint Telemetry | Windows Security Logs |
| SIEM | Splunk |
| Endpoint Monitoring | Sysmon |
| Virtualization | VirtualBox |

## Investigation Scenarios

### Scenario 01 — SMB Failed Authentication

**Status: Completed**

A controlled SMB authentication failure was generated from the Kali Linux test system against the Windows target.

The investigation correlated:

- SMB2 network traffic
- NTLM authentication
- Windows Security Event ID 4625
- Source IP address
- Source port
- Target account
- Logon Type 3
- Authentication failure reason

The evidence demonstrated network-to-endpoint correlation for the same failed SMB authentication event.

**MITRE ATT&CK:** T1021.002 — SMB/Windows Admin Shares

[View Scenario 01 Investigation](Documentation/Scenario01_SMB_Failed_Authentication.md)

### Scenario 02 — Suspicious PowerShell Network Activity

**Status: Planned / Not Completed**

This scenario was started during the original lab work but was not completed after the lab environment was lost.

It is intentionally not presented as completed evidence.

## Investigation Methodology

The investigation follows a basic SOC workflow:

1. Generate controlled activity
2. Capture network telemetry
3. Review endpoint telemetry
4. Identify relevant indicators
5. Correlate network and endpoint evidence
6. Build detection logic
7. Assess severity
8. Document findings
9. Preserve supporting evidence

## Evidence Handling

Only sanitized evidence suitable for public viewing is included in this repository.

Raw packet captures and evidence containing authentication information are retained privately and are not published.

## Project Status

| Component | Status |
|---|---|
| Network investigation fundamentals | Completed |
| Wireshark analysis | Completed |
| SMB investigation | Completed |
| Network-to-endpoint correlation | Completed |
| Scenario 01 documentation | Completed |
| Scenario 02 | Not completed |
| Full Project 5 | In progress |

## Disclaimer

All security testing was performed in an isolated laboratory environment using systems and accounts created for testing purposes.
