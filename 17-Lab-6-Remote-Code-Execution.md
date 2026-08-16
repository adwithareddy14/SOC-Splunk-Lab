\# Page 17: Lab 6 – Detecting \& Generating Alerts on Application Crashes Using Remote Code Execution (RCE)



\---



\# Lab Objective



Simulate a Remote Code Execution (RCE) attempt on DVWA and detect the malicious request using Splunk.



\---



\# Environment



Ubuntu Desktop → Victim (DVWA + Apache)



Kali Linux → Attacker



Windows → Splunk SIEM



\---



\# Step 1 (Ubuntu)



Start Apache



```bash

sudo systemctl start apache2

```



Starts the Apache web server.



\---



\# Step 2 (Kali)



Open Firefox



Visit



```

http://<Ubuntu-IP>/DVWA

```



Login



```

Username : admin



Password : password

```



\---



\# Step 3 (Kali)



Set DVWA Security



```

DVWA Security



↓



Low



↓



Submit

```



Disables input filtering for demonstration.



\---



\# Step 4 (Kali)



Open



```

Command Injection

```



\---



\# Step 5 (Kali)



Enter



```

127.0.0.1 \&\& whoami

```



Click



```

Submit

```



Attempts to execute an additional system command.



(Optional)



```

127.0.0.1 \&\& id

```



\---



\# Step 6 (Ubuntu)



View Apache logs



```bash

sudo tail -f /var/log/apache2/access.log

```



Displays the incoming HTTP requests.

You should observe many consecutive requests such as:



\---



\# Step 7 (Windows - Splunk)



Search Apache logs



```

index=\* source="/var/log/apache2/access.log"

```



Shows all web requests.



\---



\# Step 8 (Windows - Splunk)



Detect RCE payloads



```

index=\* source="/var/log/apache2/access.log" ("whoami" OR "id" OR "\&\&" OR "%26%26")

```



Detects common command injection patterns.



\---



\# Step 9 (Windows - Splunk)



Create Alert



```

Save As



↓



Alert



Name : Remote Code Execution Detection



Trigger : Number of Results > 0



Schedule : Every 1 Minute



Severity : Critical

```



\---



\# Expected Result



\- Command Injection executed from Kali.

\- Apache logs generated on Ubuntu.

\- Splunk detects the malicious request.

\- Alert is triggered successfully.



\---



\# Learning Outcome



\- Understand Remote Code Execution attacks.

\- Detect command injection attempts using Apache logs.

\- Create SIEM alerts for RCE activity.



\---

