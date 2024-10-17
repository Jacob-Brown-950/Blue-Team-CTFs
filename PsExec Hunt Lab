# Incident Response: PsExec Lateral Movement Detection

## Scenario
Our Intrusion Detection System (IDS) has raised an alert indicating suspicious lateral movement activity involving the use of PsExec. As a SOC Analyst, your task is to analyze the captured network traffic stored in a PCAP file and identify the attacker’s actions and tactics.

### Elapsed Time
**00:10:36**

## Network Information
- **IP Addresses**:
  - `10.0.0.130` - Computer accessed by attacker
  - `10.0.0.133` - SMB Server
- **Suspicious Ports**:
  - `445` - SMB

## Accounts/Machines Involved
- **Marketing-PC**
- **Sales-PC**
- **Admin**

## Summary of Findings
### 1. **Suspicious File**
- `PSEXECSVC.exe`: This file was used to carry out lateral movement. It was deployed using the ADMIN file share on the target machine.

### 2. **File Shares Involved**
- **ADMIN File Share**: The attacker used this share to install the `PSEXECSVC.exe` service on the target machine.
- **IPC File Share**: This share was used for communication between the two machines via PsExec.

### 3. **Pivoting Attempt**
- The attacker attempted to pivot to `MARKETING-PC` using the previously established connections and tools but failed.
