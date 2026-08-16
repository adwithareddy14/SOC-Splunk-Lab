01\. Introduction \& Hardware Requirements



\# SOC Lab Manual



\## Page 1: Introduction \& Hardware / Software Requirements



\# Objective



This manual provides a complete step-by-step guide to build a Security Operations Center (SOC) lab environment using VMware Workstation, Kali Linux, Ubuntu Desktop, Windows Server 2019, and Splunk Enterprise.



The lab environment will be used to demonstrate the following SIEM use cases:



\- Lab 1 – Detecting Brute Force Attempts

\- Lab 2 – Detecting Ransomware Attacks

\- Lab 3 – Detecting SQL Injection Attempts

\- Lab 4 – Detecting Cross-Site Scripting (XSS)

\- Lab 5 – Detecting Broken Access Control Attempts

\- Lab 6 – Detecting Remote Code Execution (RCE)

\- Lab 7 – Detecting Network Scanning Attempts



\---



\# Lab Architecture



Host Machine (Windows 11)



│



├── VMware Workstation Pro 17



│



├── Kali Linux 2025.3 (Attacker)



│



├── Ubuntu Desktop 24.04 LTS (Victim / Web Server)



│



└── Windows Server 2019 (Splunk SIEM)



\---



\# Virtual Machine Roles



\## Kali Linux



Purpose



\- Attack Machine

\- Penetration Testing

\- Generate Attack Traffic



Tools



\- Hydra

\- SQLMap

\- Nmap

\- Nikto

\- Curl

\- Burp Suite



\---



\## Ubuntu Desktop



Purpose



\- Victim Machine

\- Web Server

\- SSH Server

\- Log Generator



Services



\- Apache2

\- PHP

\- OpenSSH

\- DVWA



\---



\## Windows Server 2019



Purpose



\- Security Information and Event Management (SIEM)



Software



\- Splunk Enterprise

\- Splunk Universal Forwarder (Optional)



Responsibilities



\- Log Collection

\- Log Analysis

\- Alert Generation

\- Dashboard Monitoring



\---



\# Hardware Requirements



Minimum



| Component | Requirement |

| --- | --- |

| Processor | Intel i5 / Ryzen 5 |

| RAM | 16 GB |

| Storage | 150 GB SSD |

| Virtualization | VT-x / AMD-V Enabled |



Recommended



| Component | Requirement |

| --- | --- |

| Processor | Intel i7 / Ryzen 7 |

| RAM | 32 GB |

| Storage | 250 GB SSD |



\---



\# Software Requirements



\## Host Machine



\- Windows 10 / Windows 11

\- VMware Workstation Pro 17



\---



\## Virtual Machines



\### Kali Linux



Version



2025.3 Rolling



RAM



2 GB



CPU



2 Cores



Disk



40 GB



Network



NAT



\---



\### Ubuntu Desktop



Version



24.04.4 LTS



RAM



4 GB



CPU



2 Cores



Disk



40 GB



Network



NAT



\---



\### Windows Server



Version



Windows Server 2019 Standard (Desktop Experience)



RAM



4 GB



CPU



2 Cores



Disk



60 GB



Network



NAT



\---



\# Software to Download



| Software | Purpose |

| --- | --- |

| VMware Workstation Pro 17 | Virtualization |

| Kali Linux ISO | Attacker VM |

| Ubuntu Desktop ISO | Victim VM |

| Windows Server 2019 ISO | SIEM VM |

| Splunk Enterprise | SIEM Platform |

| Splunk Universal Forwarder | Log Forwarding |

| Google Chrome | Browser |

| DVWA | Vulnerable Web Application |



\---



\# Network Configuration



All virtual machines will use NAT networking.



Expected IP Range



192.168.x.x



Communication



Host ↔ VMware NAT



Kali ↔ Ubuntu



Ubuntu ↔ Windows Server



Windows Server ↔ Internet



\---



\# Final VM Configuration



| Virtual Machine | RAM | CPU | Disk | Network |

| --- | --- | --- | --- | --- |

| Kali Linux | 2 GB | 2 | 40 GB | NAT |

| Ubuntu Desktop | 4 GB | 2 | 40 GB | NAT |

| Windows Server 2019 | 4 GB | 2 | 60 GB | NAT |



\---



\# Learning Outcomes



After completing this lab manual, the learner will be able to:



\- Install VMware Workstation

\- Create virtual machines

\- Configure virtual networking

\- Install Splunk Enterprise

\- Configure log collection

\- Analyze security events

\- Create SIEM dashboards

\- Develop detection rules

\- Generate Splunk alerts

\- Detect common cyber attacks



\---



\# Lab Sequence



Page 1

Introduction \& Requirements



↓



Page 2

VMware Installation



↓



Page 3

Virtual Machine Planning



↓



Page 4

Ubuntu Installation



↓



Page 5

Windows Server Installation



↓



Page 6

Network Configuration



↓



Page 7

Splunk Enterprise Installation



↓



Page 8

Ubuntu Configuration



↓



Page 9

Splunk Log Collection



↓



Pages 10–16

Labs 1–7



↓



Final

Troubleshooting Guide



\---



\# Status



☐ VMware Installed



☐ Kali Installed



☐ Ubuntu Installed



☐ Windows Installed



☐ Splunk Installed



☐ Logs Collected



☐ Lab 1 Completed



☐ Lab 2 Completed



☐ Lab 3 Completed



☐ Lab 4 Completed



☐ Lab 5 Completed



☐ Lab 6 Completed



☐ Lab 7 Completed



\---

everywhere when you see windows server 2019 use windows host machine only ( in this module we didn't use windows server 2019 )

End of Page 1

