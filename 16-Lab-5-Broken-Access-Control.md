\# Page 16: Lab 5 – Detecting \& Generating Alerts on Broken Access Control Attempts



\---



\# Lab Objective



Simulate a Broken Access Control attack and detect unauthorized access attempts using Splunk.



\---



\# Environment



Ubuntu Desktop → Victim (DVWA)



Kali Linux → Attacker



Windows Server 2019 → Splunk SIEM



\---



\# Step 1 (Ubuntu)



Start Apache



```bash

sudo systemctl start apache2

```



Starts the web server.



\---



\# Step 2 (Kali)



Open Firefox



Visit



```

http://<Ubuntu-IP>/DVWA

```



Login



```

Username: admin



Password: password

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



\---



\# Step 4 (Kali)



Attempt to directly access a restricted page.



Example:



```

http://<Ubuntu-IP>/DVWA/setup.php

```



or



```

http://<Ubuntu-IP>/DVWA/phpinfo.php

```



This simulates an unauthorized resource access attempt.



Simply opening the page doesn't exploit anything by itself. The lab is about detecting an attempt to access a sensitive resource.



Here's what happens:



1\. You open

http://192.168.70.132/DVWA/setup.php



or



http://192.168.70.132/DVWA/phpinfo.php

2\. The browser sends an HTTP GET request



Example:



GET /DVWA/setup.php HTTP/1.1

3\. Apache receives the request



Apache records it in:



/var/log/apache2/access.log



You'll see something like:



192.168.70.139 - - \[06/Aug/2026:08:10:45 +0530] "GET /DVWA/setup.php HTTP/1.1" 200 ...

4\. Splunk receives the log



Splunk indexes that Apache log.



1\. Your detection rule identifies it



Your alert searches for requests such as:



index=\* "/DVWA/setup.php"



or



index=\* "/DVWA/phpinfo.php"



If someone accesses these pages, the alert is triggered.



\---



\# Step 5 (Ubuntu)



Monitor Apache logs



```bash

sudo tail -f /var/log/apache2/access.log

```



Shows requests made to restricted pages.



\---



\# Step 6 (Windows - Splunk)



Search Apache logs



```

index=\* source="/var/log/apache2/access.log"

```



Displays web server logs.



\---



\# Step 7 (Windows- Splunk)



Search for unauthorized page access



```

index=\* source="/var/log/apache2/access.log" ("setup.php" OR "phpinfo.php")

```



Detects attempts to access restricted resources.



\---



\# Step 8 (Windows - Splunk)



Create Alert



```

Save As



↓



Alert



Name: Broken Access Control Detection



Trigger: Number of Results > 0



Schedule: Every 1 Minute



Severity: High

```



\---



\# Expected Result



\- Unauthorized page request generated.

\- Apache logs capture the request.

\- Splunk detects the access.

\- Alert is triggered successfully.

