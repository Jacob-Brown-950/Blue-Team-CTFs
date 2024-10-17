# Network Activity Investigation

## Scenario
Your organization's security team has detected a surge in suspicious network activity. There are concerns that LLMNR (Link-Local Multicast Name Resolution) and NBT-NS (NetBIOS Name Service) poisoning attacks may be occurring within your network. These attacks are known for exploiting these protocols to intercept network traffic and potentially compromise user credentials. Your task is to investigate the network logs and examine captured network traffic.

## Detected IP Addresses
The following IP addresses were identified during the investigation:

- **Potential Victims:**
  - `192.168.232.176` - Victim (received poisoned responses)
  
- **Suspected Compromised Machines:**
  - `192.168.232.162` - Received poisoned responses
  - `192.168.232.148` - Unspecified role in the investigation

- **Attacker:**
  - `192.168.232.215` - Attacker (sending constant LLMNR queries)

- **Multicast Addresses:**
  - `224.0.0.251`
  - `224.0.0.252`
  - `239.255.255.255.250`
  - `192.168.235.255`

## Suspicious Ports/Protocols
The following ports and protocols were flagged as suspicious during the investigation:

- **Ports:**
  - `445` (SMB)
  - `135` (RPC)

## Findings
- The IP address **`192.168.232.215`** is confirmed as the attacker, constantly sending LLMNR queries.
- The IP addresses **`192.168.232.162`** and **`192.168.232.176`** received poisoned responses, indicating they were targeted by the attack.
- The compromised user account identified in the investigation is **`janesmith`**, associated with the **`AccountingPC`**.
