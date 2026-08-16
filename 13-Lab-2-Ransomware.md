\# Page 13: Lab 2 – Detecting \& Generating Alerts on Simulated Ransomware Activity



\---



\# Lab Objective



Simulate ransomware behavior on Ubuntu and detect the activity using Splunk by monitoring file creation, file renaming, and encryption-related events.



\---



\# Lab Scenario



An attacker gains access to the Ubuntu machine and executes a script that encrypts user files and changes their file extensions.



Splunk should detect the suspicious activity and generate an alert.



\---



\# Lab Environment



| Machine | Purpose |

| --- | --- |

| Kali Linux | Attacker |

| Ubuntu Desktop | Victim (Files to Encrypt) |

| Windows Server 2019 | Splunk Enterprise |



\---



\# MITRE ATT\&CK



| Technique | ID |

| --- | --- |

| Data Encrypted for Impact | T1486 |



\---



\# Flow



Kali

↓



SSH Access



↓



Ubuntu



↓



Simulated Encryption Script



↓



Syslog



↓



Universal Forwarder



↓



Splunk



↓



Detection Rule



↓



Alert



\---



\# Prerequisites



✔ Ubuntu running



✔ Splunk running



✔ Universal Forwarder configured



✔ SSH working



\---



\# ==============================



\# PART 1 – Ubuntu (Victim)



\# ==============================



\## Step 1 – Create Test Folder



Machine



```

Ubuntu

```



Run



```bash

mkdir -p \~/Documents/RansomwareLab



cd \~/Documents/RansomwareLab

```



\---



\## Step 2 – Create Sample Files



Ubuntu



```bash

touch file1.txt file2.txt file3.txt



echo "SOC Lab" > important.doc



echo "Cyber Security" > notes.txt

```



Verify



```bash

ls

```



\---



\# ==============================



\# PART 2 – Kali (Attacker)



\# ==============================



\## Step 5 – Connect to Ubuntu



Machine



```

Kali

```



Run



```bash

ssh adwithareddy@192.168.70.14



```



\## run :



cd \~/Documents/RansomwareLab



\---



\## Step 3 – Create Encryption Simulation Script



```bash

nano ransomware.sh

```



Paste



```bash

\#!/bin/bash



logger "SOC LAB : Simulated ransomware execution started"



for file in \*.txt \*.doc

do

&#x20;   mv "$file" "$file.encrypted"

done



logger "SOC LAB : Files encrypted successfully"

```



Save



```

CTRL + O



ENTER



CTRL + X

```



\---



\## Step 4 – Make Script Executable



Ubuntu



```bash

chmod +x ransomware.sh

```



\---



\## Step 6 – Execute the Script



Inside SSH session 



```bash



./ransomware.sh

```



\### If it still doesn't work



Please send the output of these three commands:



```

pwd

```



```

ls

```



```

ls \~/Documents

```



Expected



```

Files renamed

```



Exit



```bash

exit

```



\---



\# ==============================



\# PART 3 – Ubuntu Verification



\# =============================



Ubuntu



Verify files



```bash

ls

```



Expected



```

file1.txt.encrypted



file2.txt.encrypted



important.doc.encrypted

```



\---



Verify Syslog in ubuntu 



```bash

tail -20 /var/log/syslog

```



Expected



```

SOC LAB : Simulated ransomware execution started



SOC LAB : Files encrypted successfully

```



\---



\# ==============================



\# PART 4 – Splunk Detection



\# ==============================



Machine



```

Windows Server

```



Open



```

Search \& Reporting

```



\---



\## Search 1



```

index=\* "SOC LAB"

```



Expected



```

Simulation logs

```



\---



\## Search 2



```

index=\* encrypted

```



\---



\## Search 3



```

index=\* ransomware

```



\---



\# Detection Query



```

index=\* ("Simulated ransomware execution started" OR "Files encrypted successfully")



| stats count by host

```



\---



\# Create Alert



Search



↓



Save As



↓



Alert



\---



| Field | Value |

| --- | --- |

| \*\*Title\*\* | `Simulated Ransomware Detection` |

| \*\*Alert Type\*\* | `Scheduled` |

| \*\*Schedule\*\* | `Run Every Minute` \*(Recommended)\* |

| \*\*Time Range\*\* | `Last 5 minutes` |

| \*\*Cron Expression\*\* \*(if using Cron Schedule)\* | \* \* \* \* \*  |

| \*\*Expires\*\* | `24 hours` |

| \*\*Trigger alert when\*\* | `Number of Results` |

| \*\*Condition\*\* | `is greater than` |

| \*\*Value\*\* | `0` |



\---



\# Test the Alert



Repeat



Ubuntu



```bash

./ransomware.sh

```



Wait one minute.



Open



```

Activity



↓



Triggered Alerts

```



Expected



```

Simulated Ransomware Detection

```



\---



\# Verification Checklist



\- \[ ]  Test files created

\- \[ ]  Script executed

\- \[ ]  Files renamed

\- \[ ]  Syslog generated

\- \[ ]  Logs forwarded

\- \[ ]  Detection query works

\- \[ ]  Alert triggered



\---



\# Machine-wise Summary



\## Kali



```bash

ssh adwithareddy@192.168.70.144

```



Execute



```bash

cd \~/Documents/RansomwareLab



./ransomware.sh

```



\---



\## Ubuntu



Create files



Create script



Verify renamed files



Check syslog



\---



\## Windows Server



Run SPL searches



Create alert



Verify alert



\---



\# Learning Outcome



After completing this lab, you will be able to:



\- Simulate ransomware behavior safely.

\- Generate forensic evidence using Syslog.

\- Detect ransomware-like activity in Splunk.

\- Create and validate a Splunk alert for ransomware indicators.



\---



\# Next Lab



📄 \*\*Page 17 – Lab 3: Detecting \& Generating Alerts on SQL Injection Attempts\*\*

