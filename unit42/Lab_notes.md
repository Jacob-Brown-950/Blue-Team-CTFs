# HackTheBox Challenge - Unit 42

## Scenario
In this challenge, you will familiarize yourself with **Sysmon logs** and various useful EventIDs for identifying and analyzing malicious activities on a Windows system. Inspired by Palo Alto's Unit42 research on an UltraVNC campaign, the challenge guides participants through the initial access stage of the attack. The attackers utilized a backdoored version of UltraVNC to maintain access to systems.

## Tools & Setup
- **Splunk**: I used Splunk to take advantage of its data query language. You can sign up for a free enterprise trial [here](https://www.splunk.com/).
- **Sysmon**: Installed to monitor Windows events and capture key EventIDs.

## Investigation Steps

1. **Analyzing File Creation**:
   - I examined **Event ID 1** to identify file creations. There were only a few logs to sift through, so I manually inspected them.
   - A suspicious file named `"Preventivo24"` was detected. 

2. **Tracing the Source**:
   - Initially, I couldn't pinpoint where the file originated. After further investigation, I traced it back to **Dropbox**. Additionally, a community member on VirusTotal flagged the file.

3. **Detecting Anti-Forensic Techniques**:
   - The attacker employed **time stomping**, a technique that alters file timestamps to obfuscate the file’s origin. Sysmon’s **Event ID 2** tracks such changes.
   - The timestamp of the PDF file was modified from `2024-02-14 03:41:58` to `2024-01-14 08:10:06.029`, making it appear as if it was created a month earlier.

4. **Suspicious Command Execution**:
   - The `once.cmd` file was created on disk at the following path:
     ```
     C:\Users\CyberJunkie\AppData\Roaming\Photo and Fax Vn\Photo and vn 1.1.2\install\F97891C\WindowsVolume\Games\once.cmd
     ```

5. **Network Activity**:
   - The `"Preventivo24"` file attempted to reach out to both:
     - Domain: `www.example.com`
     - External IP: `93.184.216.34`
   - This was identified using **Event ID 22** (DNS query) and **Event ID 3** (Network connection).

6. **Process Termination**:
   - The file also terminated itself. This was captured using **Event ID 5**.

## Resources
- [Sysmon Documentation](https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon)
- [Splunk Free Enterprise Trial](https://www.splunk.com/)
