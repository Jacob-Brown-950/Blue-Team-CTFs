## Scenario
An anomaly was discovered within our company's intranet as the Development team found an unusual file on one of our web servers. Suspecting potential malicious activity, the network team prepared a pcap file with critical network traffic for analysis by the security team. The task was to analyze this pcap and identify potential vulnerabilities exploited by an attacker.

## Analysis Duration
- **Elapsed Time**: 00:04:53

## Key Findings

### Top IP Addresses
- **24.49.63.79** - Apache Web Server (Ubuntu OS)
- **117.11.88.124** - Suspicious external IP

### Suspicious Ports/Protocols
- **HTTPS**: 443
- **HTTP**: 80
- **Web Server**: 8080

### Malicious Upload
- **File Uploaded**: `image.jpg.php`
  - **Description**: This file acts as a backdoor for persistence, allowing the attacker continued access to the system.
  - **Upload Directory**: `reviews/uploads/`
  - **Port Used**: 8080

### Targeted File
- **Attempted Access**: The attacker was attempting to gain access to the `passwd` file, indicating a possible attempt to escalate privileges or extract sensitive information.
