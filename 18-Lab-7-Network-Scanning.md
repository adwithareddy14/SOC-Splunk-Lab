\# Page 18: Lab 7 – Detecting \& Generating Alerts on Network Scanning Attempts



\---



\# Lab Objective



Simulate a network scan using Nmap from Kali Linux and detect the scanning activity in Splunk using SSH and Apache logs.



\---



\# Why are we doing this?



Attackers usually perform network scanning before launching an attack to discover open ports and running services. Detecting reconnaissance activities early helps SOC analysts stop attacks before exploitation.



\---



\# Environment



| Machine | Role |

| --- | --- |

| Kali Linux | Attacker |

| Ubuntu Desktop | Victim |

| Windows | Splunk SIEM |



\---



\# Step 1 (Ubuntu)



Verify SSH service.



```bash

sudo systemctl status ssh

```



Checks whether SSH is running.



\---



\# Step 2 (Ubuntu)



Verify Apache service.



```bash

sudo systemctl status apache2

```



Checks whether Apache is running.



\---



\# Step 3 (Kali)



Find the Ubuntu IP.



```bash

ping <Ubuntu-IP>

```



Verifies connectivity before scanning.



\---



\# Step 4 (Kali)



Perform a TCP SYN scan.



```bash

sudo nmap -sS <Ubuntu-IP>

```



Scans the most common TCP ports.



\---



\# Step 5 (Kali)



Perform a service version scan.



```bash

sudo nmap -sV <Ubuntu-IP>

```



Identifies services running on open ports.



\---



\# Step 6 (Kali)



Perform a complete TCP port scan.



```bash

sudo nmap -p- <Ubuntu-IP>

```



Scans all 65535 TCP ports.



\---



\# Step 7 (Ubuntu)



Verify logs.



```bash

sudo tail -f /var/log/auth.log

```



Displays SSH-related log activity.



(Optional)



```bash

sudo tail -f /var/log/apache2/access.log

```



Displays web server requests.



\---



\# Step 8 (Windows - Splunk)



Search all events.



```

index=\*

```



Displays all collected logs.



\---



\# Step 9 (Windows - Splunk)



Search for Nmap User-Agent.



```

index=\* "Nmap"

```



Detects scans that access HTTP services with the default Nmap User-Agent.



\---



\# Step 10 (Windows - Splunk)



Search for SSH connection attempts.



```

index=\* source="/var/log/auth.log"

```



Displays SSH events that may indicate reconnaissance.



\---



\# Step 11 (Windows - Splunk)



Create Alert.



```

Save As



↓



Alert



Name : Network Scan Detection



Trigger : Number of Results > 0



Schedule : Every 1 Minute



Severity : Medium

```



Creates an alert when scanning activity is detected.



\---



\# Expected Result



\- Kali performs an Nmap scan.

\- Ubuntu records service access attempts.

\- Splunk receives the logs.

\- Detection query identifies scanning activity.

\- Alert is triggered.



\---



\# Verification Checklist



\- \[ ]  SSH Running

\- \[ ]  Apache Running

\- \[ ]  Nmap Scan Executed

\- \[ ]  Logs Generated

\- \[ ]  Logs Received in Splunk

\- \[ ]  Detection Query Working

\- \[ ]  Alert Triggered



\---



\# Learning Outcome



After completing this lab, you will be able to:



\- Perform network reconnaissance using Nmap.

\- Analyze scan-related logs.

\- Detect reconnaissance activity in Splunk.

\- Create SIEM alerts for network scanning.



\---



This setup provides an end-to-end workflow for Attack → Log Generation → Log Forwarding → SIEM Detection → Alert Generation.

