# Incident Analysis: Web Application Attack

## Scenario
An attack was identified against our web application after the security team analyzed logs related to a suspicious IP address. The investigation revealed a series of SQL injection attempts and unauthorized access to sensitive directories, suggesting that an attacker had exploited vulnerabilities to gain access to our systems. The primary objective was to analyze all logs associated with the attacker's IP address to determine the extent and techniques used during the incident.

## Analysis Duration
- **Elapsed Time**: 00:47:12

## Key Findings

### Attacker's IP Address
- **Malicious IP**: `111.224.250.131`  
  - Description: Associated with unauthorized activity.

### Interesting IPs
- **Legitimate Server IP**: `73.124.22.98`  
  - **Description**: Apache/2.4.52 (Ubuntu) Server, part of our legitimate server infrastructure.

### Geographical Origin
- **Origin City**: Shijiazhuang  
  - **Implication**: The attack's origin from a region with no expected traffic raises suspicions of a targeted attack.

### Exploited Vulnerability
- **Vulnerable Script**: `search.php`  
  - **Description**: Exploited to perform SQL injection attacks, highlighting the need for immediate remediation.

### SQL Injection Attempts
- **First SQLi Attempt**:  
  - **Request URI**: `/search.php?search=book%20and%201=1;%20--%20-`  
  - **Description**: Attempt to manipulate the search functionality to execute unauthorized SQL commands.

- **Database Access Attempt**:  
  - **Request URI**: `/search.php?search=book%27%20UNION%20ALL%20SELECT%20NULL%2CCONCAT%280x7178766271%2CJSON_ARRAYAGG%28CONCAT_WS%280x7a76676a636b%2Cschema_name%29%29%2C0x7176706a71%29%20FROM%20INFORMATION_SCHEMA.SCHEMATA--%20-`  
  - **Description**: Attempt to retrieve sensitive database schema information.

### Data Compromise
- **Compromised Table**:  
  - **Table Name**: `customers`  
  - **Implication**: Exposure of user data in this table poses significant risks to user privacy and organizational reputation.

### Unauthorized Access Points
- **Discovered Directory**:  
  - **Directory Name**: `/admin/`  
  - **Implication**: Indicates a potential entry point for unauthorized access to sensitive functionalities.

### Credential Compromise
- **Credentials Used**:  
  - **Username**: `admin`  
  - **Password**: `admin123!`  
  - **Implication**: Weak credentials highlight the need for stronger password policies and multifactor authentication.

### Malicious Upload
- **File Uploaded**: `NVri2vhp.php`  
  - **Description**: Likely serves as a backdoor, enabling the attacker to maintain access and control over the compromised server.

### Suspicious Port(s)
- **Port Used**:  
  - **HTTP Port**: `80`  
  - **Implication**: Standard HTTP traffic used for the attack, potentially evading detection by blending in with legitimate traffic.

## Conclusion
The analysis of the incident involving IP address `111.224.250.131` revealed multiple vulnerabilities exploited through SQL injection techniques and unauthorized access to sensitive directories. Immediate actions should be taken to patch the identified vulnerabilities, strengthen access controls, and review security policies to prevent future attacks.
