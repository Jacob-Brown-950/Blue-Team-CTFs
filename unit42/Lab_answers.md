# HackTheBox Challenge - Unit 42

## Task Answers

### Task 1
**How many Event logs are there with Event ID 11?**  
`56`

### Task 2
Whenever a process is created in memory, an event with Event ID 1 is recorded with details such as command line, hashes, process path, parent process path, etc. This information is very useful for an analyst because it allows us to see all programs executed on a system, which means we can spot any malicious processes being executed.

**What is the malicious process that infected the victim's system?**  
`C:\Users\CyberJunkie\Downloads\Preventivo24.02.14.exe.exe`

### Task 3
**Which Cloud drive was used to distribute the malware?**  
`dropbox`

### Task 4
The initial malicious file time-stamped (a defense evasion technique, where the file creation date is changed to make it appear old) many files it created on disk.

**What was the timestamp changed to for a PDF file?**  
`2024-01-14 08:10:06`

### Task 5
The malicious file dropped a few files on disk.

**Where was "once.cmd" created on disk? Please answer with the full path along with the filename.**  
`C:\Users\CyberJunkie\AppData\Roaming\Photo and Fax Vn\Photo and vn 1.1.2\install\F97891C\WindowsVolume\Games\once.cmd`

### Task 6
The malicious file attempted to reach a dummy domain, most likely to check the internet connection status.

**What domain name did it try to connect to?**  
`www.example.com`

### Task 7
**Which IP address did the malicious process try to reach out to?**  
`93.184.216.34`

### Task 8
The malicious process terminated itself after infecting the PC with a backdoored variant of UltraVNC.

**When did the process terminate itself?**  
`2024-02-14 03:41:58`
