\# 🛡️ Page 14: Lab 3 – Detecting \& Generating Alerts on SQL Injection Attempts



\---



\# Lab Objective



Simulate SQL Injection attacks against the DVWA web application hosted on Ubuntu and detect the attack using Splunk by analyzing Apache web server logs.



\---



\# Why are we doing this?



SQL Injection is one of the most common web attacks. Attackers insert malicious SQL queries into input fields to bypass authentication or access sensitive database information. A SOC analyst should be able to identify these malicious requests from web server logs.



\---



\# Environment Used



| Machine | Role | Task |

| --- | --- | --- |

| Kali Linux | Attacker | Launch SQL Injection attacks |

| Ubuntu Desktop | Victim | Hosts DVWA (Apache + PHP + MySQL) |

| Windows Server 2019 | SIEM | Detect SQL Injection attempts in Splunk |



\---



\# Attack Flow



```



Kali

(Attacker)



↓



DVWA Login/Input Page



↓



Apache Access Log



↓



Splunk Universal Forwarder



↓



Splunk Enterprise



↓



SQL Injection Detection



↓



Alert

```



\---



\# Prerequisites



\- Apache Running

\- DVWA Installed

\- Splunk Running

\- Universal Forwarder Running

\- Apache Logs Forwarded



\---



\# Step 1: Verify Apache



\## Perform on: Ubuntu



```bash

sudo systemctl status apache2

```



\*\*Explanation:\*\* Checks whether the Apache web server is running.



Expected:



```

Active (running)

```



\---



\# Step 2: Verify DVWA



\## Perform on: Kali



Open Firefox



Visit



```

<http://192.168.70.144/DVWA>

```



Login



```

Username : admin



Password : password

```



\*\*Explanation:\*\* Opens the vulnerable web application used for the SQL Injection demonstration.



\---



\# Step 3: Set Security Level



\## Perform on: Kali (DVWA Web Page)



Navigate to



```

DVWA Security

```



Select



```

Low

```



Click



```

Submit

```



\*\*Explanation:\*\* Disables input filtering so SQL Injection succeeds easily.



\---



\# Step 4: Open SQL Injection Module



\## Perform on: Kali



Navigate to



```

SQL Injection

```



\*\*Explanation:\*\* Opens the intentionally vulnerable SQL Injection page.



\---



\# Step 5: Perform SQL Injection



\## Perform on: Kali



Enter



```

1' OR '1'='1

```



Click



```

Submit

```



\*\*Explanation:\*\* Attempts to modify the SQL query so that it returns all records.



Expected



All users are displayed.



\---



\# Step 6: Perform Another Attack



\## Perform on: Kali



Input



```

' UNION SELECT user,password FROM users#

```



Click



```

Submit

```



\*\*Explanation:\*\* Attempts to retrieve usernames and passwords using a UNION query.



\---



\# Step 7: Verify Apache Logs



\## Perform on: Ubuntu



```bash

sudo tail -20 /var/log/apache2/access.log

```



\*\*Explanation:\*\* Displays the most recent HTTP requests handled by Apache.



Expected



```

GET /DVWA/vulnerabilities/sqli/...

```



\---



\# Step 8: Search Logs in Splunk



\## Perform on: Windows Server (Splunk)



Go to



```

Search \& Reporting

```



Run



```

index=\* source="/var/log/apache2/access.log"

```



\*\*Explanation:\*\* Displays all Apache access log events collected by Splunk.



\---



\# Step 9: Search for SQL Injection Keywords



Run



```

index=\* source="/var/log/apache2/access.log" ("UNION" OR "SELECT" OR "%27")

```



\*\*Explanation:\*\* Searches for common SQL Injection keywords and encoded single quotes.



Expected



Attack requests appear.



\---



\# Step 10: Detection Query



Run



```

index=\* source="/var/log/apache2/access.log"



("UNION" OR "SELECT" OR "%27" OR "OR+1%3D1")

```



\*\*Explanation:\*\* Detects requests containing typical SQL Injection patterns.



\---



\# Step 11: Create Alert



Click



```

Save As



↓



Alert

```



Configure



| Setting | Value |

| --- | --- |

| Alert Name | SQL Injection Detection |

| Trigger | Number of Results > 0 |

| Schedule | Every 1 Minute |

| Severity | High |



\*\*Explanation:\*\* Generates an alert whenever SQL Injection traffic is detected.



\---



\# Step 12: Test Alert



\## Perform on: Kali



Repeat



```

1' OR '1'='1

```



Wait one minute.



\*\*Explanation:\*\* Generates fresh attack logs to verify the alert.



\---



\# Step 13: Verify Alert



\## Perform on: Windows Server



Navigate



```

Activity



↓



Triggered Alerts

```



Expected



```

SQL Injection Detection

```



\*\*Explanation:\*\* Confirms Splunk detected the SQL Injection attack.



\---



\# Expected Result



Splunk should:



\- Receive Apache logs.

\- Detect SQL Injection keywords.

\- Trigger an alert.

\- Record attacker IP and timestamp.



\---



\# Verification Checklist



\- \[ ]  Apache Running

\- \[ ]  DVWA Accessible

\- \[ ]  SQL Injection Executed

\- \[ ]  Apache Logs Generated

\- \[ ]  Logs Received in Splunk

\- \[ ]  Detection Query Working

\- \[ ]  Alert Created

\- \[ ]  Alert Triggered



\---



\# Troubleshooting



\## Ubuntu



```bash

sudo systemctl restart apache2

```



\*\*Explanation:\*\* Restarts Apache if the web server is not responding.



\---



```bash

sudo tail -50 /var/log/apache2/access.log

```



\*\*Explanation:\*\* Verifies that Apache is logging incoming requests.



\---



\## Splunk



```

index=\* source="/var/log/apache2/access.log"

```



\*\*Explanation:\*\* Confirms Apache logs are reaching Splunk.



\---



\# Learning Outcome



After completing this lab, you will be able to:



\- Perform SQL Injection in a controlled environment.

\- Analyze Apache web server logs.

\- Detect SQL Injection using SPL queries.

\- Create Splunk alerts for web attacks.

\- Identify attacker IP addresses.



\---



\# Next Lab



📄 \*\*Page 18 – Lab 4: Detecting \& Generating Alerts on XSS Attempts\*\*

