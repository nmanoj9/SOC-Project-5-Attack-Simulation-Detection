# Scenario 01 — SMB Failed Authentication

## 1. Objective

Simulate a controlled SMB authentication failure from a Kali Linux system against a Windows host and investigate the activity using network and Windows security telemetry.

The objective is to demonstrate network-to-endpoint correlation during a SOC investigation.

---

## 2. Lab Environment

| Component | Details |
|---|---|
| Attacker/Test System | Kali Linux |
| Attacker IP | 192.168.56.10 |
| Target System | Windows |
| Target IP | 192.168.56.1 |
| Protocol | SMB2 |
| Transport | TCP |
| Destination Port | 445 |
| Authentication | NTLM |
| Test Account | SOC_Test |

The activity was performed inside an isolated VirtualBox lab environment.

---

## 3. Attack Simulation

A controlled SMB authentication attempt was performed from Kali Linux against the Windows host using the dedicated `SOC_Test` lab account and an incorrect password.

The authentication attempt resulted in:

`NT_STATUS_LOGON_FAILURE`

This was a single controlled failed authentication attempt.

It was not classified as brute force because repeated authentication attempts were not generated for this scenario.

---

## 4. Network Evidence

Wireshark captured the SMB2 authentication exchange between:

- Source: `192.168.56.10` — Kali
- Destination: `192.168.56.1` — Windows
- Destination Port: `445/TCP`

The captured sequence included:

1. SMB2 negotiation
2. NTLMSSP negotiation
3. NTLM challenge
4. NTLM authentication request for `SOC_Test`
5. `STATUS_LOGON_FAILURE` response

This demonstrates that the connection progressed beyond simple TCP connectivity into an SMB authentication exchange.

---

## 5. Windows Security Evidence

Windows Security Event ID `4625` recorded the failed network logon.

Important fields included:

- Event ID: `4625`
- Account: `SOC_Test`
- Logon Type: `3`
- Source IP: `192.168.56.10`
- Workstation: `KALI`
- Authentication Package: `NTLM`
- Failure reason: Unknown user name or bad password

Logon Type 3 indicates a network logon.

---

## 6. Investigation Timeline

The controlled SMB authentication attempt was generated from Kali Linux against the Windows target.

Windows recorded the failed authentication at:

19-Aug-2026 16:57:41

Windows Event ID:

4625

The event identified:

- Source IP: 192.168.56.10
- Source Port: 55024
- Target Account: SOC_Test
- Logon Type: 3
- Authentication Package: NTLM
- Failure Reason: Unknown user name or bad password
- Workstation: KALI

Wireshark captured the corresponding SMB2 authentication failure traffic.

The relevant Wireshark packet was observed approximately 2.65 seconds after the Windows event timestamp.

The Wireshark traffic identified:

- SMB2 Session Setup Response
- STATUS_LOGON_FAILURE (0xc000006d)
- Account: SOC_Test
- Source/Destination context consistent with the Windows event
- Destination Port: 55024

The source port 55024 provides an additional correlation point between the network and endpoint evidence.


## 7. Evidence Correlation

Correlation 1 — Network to Endpoint

Wireshark captured the SMB authentication failure, while Windows Security independently recorded Event ID 4625.

This provides network-to-endpoint corroboration.

Correlation 2 — Source

Wireshark and Windows both identify:

192.168.56.10

as the source system.

Correlation 3 — Account

Both sources identify:

SOC_Test

as the account involved in the authentication attempt.

Correlation 4 — Service

The network traffic shows:

SMB2 → TCP/445 → NTLM

The Windows event shows:

Logon Type 3 → NTLM

These observations are consistent with the same remote SMB authentication activity.


## 8. Investigation Findings

The activity originated from the Kali Linux host and targeted the Windows host over TCP/445.

The connection progressed into an SMB2/NTLM authentication exchange involving the SOC_Test account.

The authentication failed, producing STATUS_LOGON_FAILURE in the network capture and Event ID 4625 on the Windows endpoint.

The available evidence does not indicate successful authentication or system compromise.


## 9. Detection Logic

A potential detection can correlate:

- Windows Event ID 4625
- Remote/network logon (Logon Type 3)
- SMB-related activity
- Source IP
- Target account
- Repeated authentication failures

A single failed authentication should generally be treated as an authentication anomaly rather than automatically classified as brute force.

Repeated failures from the same source against one or multiple accounts would increase the severity and could indicate brute-force or password-spraying activity.


## 10. Severity

Lab classification: Informational / Low

Reason:

- Activity was intentionally generated.
- The source was the known Kali lab system.
- The target account was a dedicated lab account.
- The authentication failed.
- No successful compromise was observed.

In a real environment, severity would depend on source reputation, account privilege, frequency, authentication success, lateral-movement indicators, and surrounding endpoint activity.


## 11. MITRE ATT&CK Mapping

T1021.002 — SMB/Windows Admin Shares

SMB is commonly associated with Windows remote services and lateral movement.

However, this lab scenario demonstrates a failed authentication attempt only.

Successful lateral movement was not demonstrated.


## 12. Analyst Conclusion

A controlled SMB authentication attempt originating from the Kali Linux host (192.168.56.10) targeted the Windows host (192.168.56.1) over TCP/445.

Wireshark captured the SMB2/NTLM authentication exchange and recorded STATUS_LOGON_FAILURE for the SOC_Test account.

Windows Security Event ID 4625 independently recorded the failed remote logon from the same source IP and account.

The network and endpoint telemetry therefore corroborate the same failed SMB authentication event.

The activity is classified as a failed SMB authentication attempt rather than brute force because only a single controlled failure was generated.


## 13. Evidence References

Public evidence:

- 02_Wireshark_SMB_Authentication_Failure.png
- 03_Wireshark_SMB2_Status_Logon_Failure.png
- 04_Windows_Event_4625_Failed_Logon.png

Private evidence:

- 01_Kali_SMB_Failed_Authentication.png
- 05_SMB_Failed_Authentication.pcapng

The raw PCAP is retained privately and is not intended for public GitHub publication.

The Kali screenshot containing authentication credentials is also retained privately.


## 14. Privacy and Security Notes

The lab uses the private VirtualBox network 192.168.56.0/24.

Only sanitized screenshots should be published publicly.

The raw PCAP should remain private because packet captures may contain additional network metadata that is not visible in selected screenshots.

Passwords, credentials, personal usernames, hostnames, public IP addresses, tokens, and other identifying information must not be published.
