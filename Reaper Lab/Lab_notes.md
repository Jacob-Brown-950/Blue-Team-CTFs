# Suspicious Logon Investigation - MITM Attack Analysis

## Scenario
Our SIEM alerted us to a suspicious logon event that requires immediate investigation. The alert indicated a mismatch between the **IP Address** and the **Source Workstation Name**. We have been provided with a network capture (PCAP file) and event logs from the timeframe surrounding the incident. The objective is to correlate the given evidence and report findings.

## Tools Used
- **Splunk**: For log analysis and event correlation.
- **Wireshark**: For packet capture (PCAP) analysis.

## Summary of Findings

### 1. **Top IP Addresses Identified**
| IP Address      | Hostname           |
|-----------------|--------------------|
| 172.17.79.129   | Forela-Wkstn001    |
| 172.17.79.136   | Forela-Wkstn002    |
| 172.17.79.135   | MITM Address       |

- The IP `172.17.79.135` was identified as a **Man-in-the-Middle (MITM)** address that intercepted user credentials.

### 2. **Top Ports Observed**
| Port Number     | Protocol           | Usage                      |
|-----------------|--------------------|
| 445             | SMB                | Access to shared files     |
| 443             | HTTPS              | Encrypted communications   |
| 389             | LDAP               | Directory services         |

These ports indicate that the attacker might have been attempting to access shared resources and sensitive information using these services.

### 3. **User Impacted**
- **Username**: Arthur Kyle
- Arthur Kyle's credentials were intercepted by the MITM attack.

### 4. **Actions Taken by the User**
- The user attempted to access a **file tree** on the Domain Controller and also tried accessing a **shared drive**. 
- This activity aligns with the logon event captured in the event logs, which was flagged due to the **IP and workstation name mismatch**.

## Evidence Correlation
Using Splunk, I isolated the log entry that corresponded to Arthur Kyle’s login attempt. From this log, I extracted the IP details, user actions, and timestamp, which all matched the timeframe and behavior expected of a MITM attack. Wireshark analysis further confirmed the interception and redirection of traffic by the attacker at `172.17.79.135`.

## Conclusion
Based on the correlation of network capture data and event logs:
- A **MITM attack** intercepted Arthur Kyle’s credentials while he accessed the Domain Controller’s file tree.
- Immediate measures should be taken to secure affected systems and identify potential vulnerabilities that allowed this attack vector.
