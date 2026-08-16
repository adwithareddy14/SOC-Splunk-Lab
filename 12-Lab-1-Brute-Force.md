\# Page 12: Lab 1 – Detecting \& Generating Alerts on Brute-Force Attempts



\---



\# Lab Objective



Detect SSH brute-force login attempts against Ubuntu using Splunk Enterprise and generate an alert when multiple failed login attempts are observed.



\---



\# Attack Scenario



An attacker attempts to gain unauthorized access to the Ubuntu server by repeatedly trying different passwords over SSH.



Ubuntu records all failed authentication attempts in:



```



/var/log/auth.log

```



These logs are forwarded to Splunk using the Universal Forwarder.



Splunk detects multiple failed login attempts and generates an alert.



\---



\# Lab Topology



```



Kali Linux

(Attacker)



↓



SSH Brute Force



↓



Ubuntu

SSH Server



↓



/var/log/auth.log



↓



Universal Forwarder



↓



Splunk Enterprise



↓



Detection Rule



↓



Alert

```



\---



\# Prerequisites



✔ Ubuntu SSH Server Running



✔ Splunk Enterprise Running



✔ Universal Forwarder Configured



✔ auth.log being forwarded



\---



\# Step 1: Verify SSH Service



Ubuntu



```bash

sudo systemctl status ssh

```



Expected



```

Active (running)

```



\---



\# Step 2: Verify SSH Connectivity



From Kali



```bash

ssh adwithareddy@192.168.70.144

```



Exit



```bash

exit

```



\---



\# Step 3: Generate Brute-Force Attempts



From Kali



```bash

ssh adwithareddy@192.168.70.144

```



Enter an incorrect password.



Repeat this \*\*10–15 times\*\*.



Each failed attempt creates an event in:



```

/var/log/auth.log

```



\---



\# Step 4: Verify Ubuntu Logs



Ubuntu



```bash

tail -20 /var/log/auth.log

```



Expected



```

Failed password



Invalid user



authentication failure

```



\---



\# Step 5: Verify Logs in Splunk



Open



```

Search \& Reporting

```



Search



```

index=\* source="/var/log/auth.log"

```



Expected



SSH authentication logs appear.



\---



\# Step 6: Detect Failed Login Attempts



Run



```

index=\* source="/var/log/auth.log" "Failed password"

```



Expected



Only failed SSH logins.



\---



\# Step 7: Count Failed Attempts



```

index=\* source="/var/log/auth.log" "Failed password"

| rex "Failed password for (?<user>\\S+) from (?<src>\\d+\\.\\d+\\.\\d+\\.\\d+)"

| stats count by src user

```



Expected



| Source IP | Username | Count |

| --- | --- | --- |

| Kali IP | adwithareddy | 15 |



\---



If any IP generates five or more failed logins, it is flagged as a brute-force attempt.



\---



\# Step 9: Create Splunk Alert



Navigate



```

Search \& Reporting



↓



Run Detection Query



↓



Save As



↓



Alert

```



Run detection query : 



```

index=\* source="/var/log/auth.log" "Failed password"

| rex "Failed password for (?<user>\\S+) from (?<src>\\d+\\.\\d+\\.\\d+\\.\\d+)"

| stats count by src user

| where count >= 5

```



click save as , and then proceed - Alert Name



Configure the alert as follows:



| Setting | Value |

| --- | --- |

| Alert Name | SSH Brute Force Detection |

| Permissions | Private |

| Alert Type | Scheduled |

| Schedule | Cron Schedule |

| Cron Expression | \*/1 \* \* \* \* |

| Trigger Condition | Number of Results > 0 |

| Time Range | Last 5 Minutes |

| Severity | High |

|  |  |



Click \*\*Save\*\*.



\---



\# Step 10: Test the Alert



Generate another 10 failed SSH login attempts from Kali.



Wait one minute.



Navigate



```

Alerts



↓



Brute Force Attempt 

```



If the attack is detected, the \*\*Trigger History\*\* section will display a new event.



!image.png



\---



\# Verification Checklist



\- \[ ]  SSH Running

\- \[ ]  Failed Logins Generated

\- \[ ]  auth.log Updated

\- \[ ]  Logs Visible in Splunk

\- \[ ]  Detection Query Working

\- \[ ]  Alert Created

\- \[ ]  Alert Triggered



\---



\# Troubleshooting



\## No SSH Logs



Ubuntu



```bash

sudo tail -50 /var/log/auth.log

```



\---



\## No Logs in Splunk



Restart Universal Forwarder



```bash

sudo /opt/splunkforwarder/bin/splunk restart

```



\---



\## Alert Not Triggering



Check



\- Time Range

\- Search Query

\- Trigger Condition

\- Receiving Port 9997



\---



\# Learning Outcome



After completing this lab, you will be able to:



\- Generate SSH brute-force attacks in a controlled environment.

\- Analyze Linux authentication logs.

\- Write SPL detection queries.

\- Create and test Splunk alerts.

\- Identify attacking IP addresses.

\- Detect brute-force attacks using SIEM.



\---



\# Next Lab



\*\*Page 16 – Lab 2: Detecting \& Generating Alerts on Ransomware Attacks\*\*

