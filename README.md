# SOC Investigation & Threat Detection Using Splunk SIEM
### Pramodh Prakash | MSc Cybersecurity NTU UK 

## About This Project
Hands-on SOC investigation using Splunk SIEM on two simulated enterprise cyberattacks using real Windows Security Event IDs and MITRE ATT&CK attack patterns.

## Analyst
| Field | Details |
|-------|---------|
| Name | Pramodh Prakash |
| Education | MSc Cybersecurity — Nottingham Trent University UK |
| Experience | 1 Year — Network Engineer, Cisco |

## Attacks Investigated

### Investigation 1 — Brute Force + Credential Theft
- RDP brute force on admin account from 192.168.1.50
- mimikatz.exe executed — credential dumping
- backdoor_user account created and added to Administrators
- Scheduled task created for persistence
- Audit log cleared — Event 1102

### Investigation 2 — Ransomware + Insider Threat
- RDP brute force on james.wilson from 45.33.32.156
- ransomware_payload.exe executed — 5 files encrypted
- Backdoor account backdoor_svc created
- Insider threat — emma.davis exfiltrated 10.3MB via FTP
- Audit log cleared — Event 1102

## Tools Used
- Splunk SIEM
- SPL — Search Processing Language
- Windows Security Event Logs

## MITRE ATT&CK Coverage
| Tactic | Technique | ID |
|--------|-----------|-----|
| Initial Access | Brute Force | T1110 |
| Execution | PowerShell | T1059.001 |
| Credential Access | Mimikatz | T1003 |
| Persistence | Create Account | T1136.001 |
| Persistence | Scheduled Task | T1053.005 |
| Defense Evasion | Clear Logs | T1070.001 |
| Exfiltration | FTP Exfiltration | T1048 |
| Impact | Ransomware | T1486 |

## Key SPL Queries Used
index=main source="windows_security.log" "Failed Login"
index=main source="windows_security.log" "Successful Login"
index=main source="windows_security.log" 4688
index=main "Failed Login" | stats count by host
index=main source="windows_security.log" mimikatz.exe
index=main source="investigation3.log" ransomware
index=main source="investigation3.log" ftp
index=main 1102
index=main source="investigation3.log" 3389
Many more as well

## Repository Structure
Splunk-SOC-Investigation/

├── README.md

├── logs/

│   ├── windows_security.log

│   └── investigation3.csv

├── screenshots/

│   └── screenshots

└── SOC_Investigation_Report_Pramodh.pdf

## Disclaimer
Log files were simulated using real Windows Security 
Event IDs and MITRE ATT&CK attack patterns for 
educational and portfolio purposes.
