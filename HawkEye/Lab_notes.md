# Incident Analysis: Phishing Campaign Leading to Data Exfiltration

## Scenario

An accountant at the organization received a phishing email containing a download link for an invoice. Shortly after opening the email and accessing the download link, suspicious network traffic was observed. Upon investigation, it was revealed that the downloaded file was malicious and led to data exfiltration. This report details the observed malicious activity, protocols and ports used, and analysis of the compromised information.

## Summary of the Incident

- **Victim Device**: BEIJING-5CD1-PC (Internal IP: 10.4.10.132)
- **Compromised User**: Roman McGuire
- **Timeframe**: 20:37:54 - 21:40:04 UTC
- **Malicious Domain**: proforma-invoices.com
- **Malware Identified**: `tkraw_Protected99.exe` (Trojan - HawkEye Keylogger)

## Top Protocols/Ports Observed

| Protocol/Port   | Description                      |
| --------------- | -------------------------------- |
| **SMTP**        | Email communication used for exfiltration |
| **SMB**         | File sharing and network access  |
| **HTTP (80)**   | Malware download and communication |
| **HTTPS (443)** | Encrypted traffic to C2 server   |
| **445**         | SMB traffic                      |
| **587**         | SMTP submission for email transmission |

## Network Indicators

| IP Address       | Description                                 |
| ---------------- | ------------------------------------------- |
| 217.182.138.150  | Malicious IP associated with exfiltration activity |
| 23.229.162.69    | Mail server used for sending stolen credentials |
| 10.4.10.132      | Compromised internal host (BEIJING-5CD1-PC) |
| 10.4.10.4        | Internal network traffic (possibly SMB/File server) |

## Domain Analysis

| Domain                  | Classification  |
| ----------------------- | --------------- |
| proforma-invoices.com   | Malicious       |
| macwinlogistics.in      | Associated with exfiltration activity |

### Decoded Credentials and Email Communication

From the pcap analysis, several communications were detected between BEIJING-5CD1-PC and external servers. The credentials decoded from the captured traffic reveal a concerning exfiltration pattern. The following email credentials were compromised and sent externally:

- **Email**: `sales.del@macwinlogistics.in`
- **Password**: `Sales@23`

**Note**: Passwords associated with the victim, Roman McGuire, were exfiltrated to this email address.

## Key Malware Findings

The analysis of the traffic revealed that the downloaded file, `tkraw_Protected99.exe`, is a variant of **HawkEye Keylogger**. This malware is typically delivered via phishing campaigns and is designed to capture user credentials, email information, and other sensitive data. 

### Indicators Found

1. **File Details**:
   - **File Name**: `tkraw_Protected99.exe`
   - **File Hash**: Marked as malicious (Trojan Malware)
   - **Behavior**: Queries "whatismyipaddress.com" to confirm external IP details

2. **HawkEye Keylogger Details**:
   - Version: **Reborn v9**
   - Captured data includes various credentials, system details, and activity logs of the compromised user.

## Compromised Data

Below is a summary of the compromised data captured by the malware:

### Extracted Passwords

1. **Bank of America**:
   - **URL**: `https://www.bankofamerica.com/`
   - **Browser**: Chrome
   - **Username**: roman.mcguire
   - **Password**: `P@ssw0rd$`

2. **AOL Email**:
   - **URL**: `https://login.aol.com/account/challenge/password`
   - **Browser**: Internet Explorer 7.0 - 9.0
   - **Username**: roman.mcguire914@aol.com
   - **Password**: `P@ssw0rd$`

3. **Outlook Account**:
   - **Application**: MS Outlook 2002/2003/2007/2010
   - **Email**: roman.mcguire@pizzajukebox.com
   - **Password**: `P@ssw0rd$`
   - **Server**: smtp.pizzajukebox.com (Port: 587)

## Incident Timeline

1. **20:37:54 UTC**:
   - User accessed the domain **proforma-invoices.com** and downloaded the file `tkraw_protected00.exe`, which is classified as **HawkEye Keylogger**.
   
2. **20:38:15 UTC**:
   - `tkraw_Protected99.exe` was executed on BEIJING-5CD1-PC, initiating outbound connections to **whatismyipaddress.com**.
   
4. **20:38:16 UTC**:
   - Credentials from various web services (e.g., AOL, Bank of America, Outlook) were sent to the email address **sales.del@macwinlogistics.in**.

5. **21:40:04 UTC**:
   - The malicious activity ceased, with the final SMTP communication sent to **23.229.162.69**.
  
6. **20:37:54 - 21:40:04**
   - Time length of compromise

## Recommendations

1. **Isolate the Compromised Host**:
   - Disconnect BEIJING-5CD1-PC from the network immediately to prevent further exfiltration.

2. **Scan for Indicators of Compromise (IOCs)**:
   - Use the identified file hashes, IP addresses, and domain names as IOCs to scan other devices for similar threats.

3. **Reset Credentials**:
   - Ensure that Roman McGuire and any associated accounts reset their credentials across all platforms.

4. **Implement Email Filtering**:
   - Improve email filtering mechanisms to detect and quarantine suspicious attachments and links from untrusted domains.

5. **Network Monitoring**:
   - Monitor outbound network traffic for unusual patterns, particularly traffic involving suspicious domains like **proforma-invoices.com**.

---

By following these recommendations, the organization can mitigate the immediate risk posed by this phishing attack and prevent future incidents involving similar tactics.
