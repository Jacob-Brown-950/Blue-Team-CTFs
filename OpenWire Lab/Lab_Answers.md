## Here are the Questions and Answers

### Q1
By identifying the C2 IP, we can block traffic to and from this IP, helping to contain the breach and prevent further data exfiltration or command execution. Can you provide the IP of the C2 server that communicated with our server?

**Answer:** `146.190.21.92`



### Q2
Initial entry points are critical to trace back the attack vector. What is the port number of the service the adversary exploited?

**Answer:** `61616`



### Q3
Following up on the previous question, what is the name of the service found to be vulnerable?

**Answer:** `Apache ActiveMQ`



### Q4
The attacker's infrastructure often involves multiple components. What is the IP of the second C2 server?

**Answer:** `128.199.52.72`



### Q5
Attackers usually leave traces on the disk. What is the name of the reverse shell executable dropped on the server?

**Answer:** `docker`



### Q6
What Java class was invoked by the XML file to run the exploit?

**Answer:** `java.lang.ProcessBuilder`



### Q7
To better understand the specific security flaw exploited, can you identify the CVE identifier associated with this vulnerability?

**Answer:** `CVE-2023-46604`



### Q8
What is the vulnerable Java method and class that allows an attacker to run arbitrary code? (Format: Class.Method)

**Answer:** `BaseDataStreamMarshaller.createThrowable`
