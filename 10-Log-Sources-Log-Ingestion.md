\# 📥 Page 10: Configuring Log Sources \& Validating Log Ingestion



\---



\# Objective



Configure Ubuntu to generate useful logs and verify that Splunk Enterprise is successfully receiving and indexing them.



After completing this page:



\- SSH logs are forwarded

\- Apache logs are forwarded

\- System logs are forwarded

\- Splunk receives all events successfully



\---



\# Lab Architecture



```



Kali Linux

(Attacker)

│

│ Attack Traffic

▼



Ubuntu Desktop

(Apache + DVWA + SSH)



│

│ Splunk Universal Forwarder

▼



Windows 



Splunk Enterprise

```



\---



\# Log Sources



| Log Source | Location |

| --- | --- |

| SSH Authentication | /var/log/auth.log |

| Apache Access | /var/log/apache2/access.log |

| Apache Error | /var/log/apache2/error.log |

| System Log | /var/log/syslog |



\---



\# Step 1: Verify Universal Forwarder Status



Execute



```bash

sudo /opt/splunkforwarder/bin/splunk status

```



Expected



```

splunkd is running.

```



\---



\# Step 2: Verify Forward



```bash

sudo /opt/splunkforwarder/bin/splunk list forward-server

```



Expected



```

Active

```



\---



\# Step 3: Verify Monitored Inputs



```bash

sudo /opt/splunkforwarder/bin/splunk list monitor

```



Expected



```

/var/log/auth.log



/var/log/apache2/access.log



/var/log/apache2/error.log



/var/log/syslog

```



\---



\# Step 4: Generate SSH Logs



Open another terminal.



Attempt an SSH login.



```bash

ssh localhost

```



Exit



```bash

exit

```



This generates authentication events.



\---



\# Step 5: Generate Apache Access Logs



Open Firefox.



Visit



```

<http://localhost/DVWA>

```



Refresh the page several times.



Apache access logs will be generated.



\---



\# Step 6: Generate Apache Error Logs



Request a page that does not exist.



```

<http://localhost/abc123>

```



Apache records a 404 error.



\---



\# Step 7: Generate System Logs



Execute



```bash

logger "SOC Lab Test Event"

```



This creates a custom Syslog entry.



\---



\# Step 8: Verify Local Logs



SSH Log



```bash

tail -10 /var/log/auth.log

```



Apache Access



```bash

tail -10 /var/log/apache2/access.log

```



Apache Error



```bash

tail -10 /var/log/apache2/error.log

```



System Log



```bash

tail -10 /var/log/syslog

```



\---



\# Step 9: Verify Logs in Splunk



Open



```

Search \& Reporting

```



Search



```

index=soc\_lab

```



If no custom index exists



```

index=\*

```



Expected



Events from:



\- SSH

\- Apache

\- Syslog



\---



\# Step 10: Filter SSH Events



```

index=\* auth.log

```



\---



\# Step 11: Filter Apache Access



```

index=\* access.log

```



\---



\# Step 12: Filter Apache Errors



```

index=\* error.log

```



\---



\# Step 13: Filter System Logs



```

index=\* syslog

```



\---



\# Step 14: Verify Event Count



Run



```

index=\* | stats count

```



Expected



```

Thousands of events (depending on system activity)

```



\---



\# Step 15: Verify Event Timeline



Run



```

index=\*

```



Check



\- Event timestamps

\- Host

\- Source

\- Sourcetype



Verify events are updating in real time.



\---



\# Expected Result



Splunk should now receive:



\- SSH authentication logs

\- Apache access logs

\- Apache error logs

\- System logs



All events should be searchable.



\---



\# Verification Checklist



\- \[ ]  Universal Forwarder Running

\- \[ ]  Connected to Splunk

\- \[ ]  SSH Logs Visible

\- \[ ]  Apache Access Logs Visible

\- \[ ]  Apache Error Logs Visible

\- \[ ]  Syslog Visible

\- \[ ]  Events Searchable



\---



\# Commands Summary



```bash

sudo /opt/splunkforwarder/bin/splunk status



sudo /opt/splunkforwarder/bin/splunk list forward-server



sudo /opt/splunkforwarder/bin/splunk list monitor



ssh localhost



logger "SOC Lab Test Event"



tail -10 /var/log/auth.log



tail -10 /var/log/apache2/access.log



tail -10 /var/log/apache2/error.log



tail -10 /var/log/syslog

```



\---



\# Splunk Search Commands



```

index=\*



index=\* auth.log



index=\* access.log



index=\* error.log



index=\* syslog



index=\* | stats count

```



\---



\# Troubleshooting



\## No Logs in Splunk



Restart the Universal Forwarder:



```bash

sudo /opt/splunkforwarder/bin/splunk restart

```



\---



\## Forward Server Not Active



Verify the receiving port (9997) is enabled in Splunk.



\---



\## Apache Logs Missing



Generate web traffic by accessing:



```

http://<Ubuntu-IP>/DVWA

```



\---



\## SSH Logs Missing



Attempt an SSH login:



```bash

ssh localhost

```



\---



\# Learning Outcome



After completing this page, you will be able to:



\- Validate log forwarding from Ubuntu to Splunk.

\- Search and filter logs using SPL.

\- Confirm that the SIEM environment is fully operational.

\- Verify end-to-end log ingestion.



\---

