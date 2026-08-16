\# ✅ Page 11: SOC Lab Environment Validation \& Attack Simulation



\---



\# Objective



Validate that the complete SOC lab environment is functioning correctly before beginning the Splunk SIEM detection labs.



This page verifies:



\- Network connectivity

\- Web server accessibility

\- SSH connectivity

\- DVWA functionality

\- Log forwarding

\- Splunk event ingestion



\---



\# Final Lab Topology



```



&#x20;                    Kali Linux

&#x20;                 (Attacker Machine)

&#x20;                         │

&#x20;         ┌───────────────┼────────────────┐

&#x20;         │               │                │

&#x20;         │ SSH           │ HTTP           │ Nmap

&#x20;         ▼               ▼                ▼

&#x20;               Ubuntu Desktop

&#x20;       (Apache + DVWA + SSH + Logs)

&#x20;                    │

&#x20;                    │ Universal Forwarder

&#x20;                    ▼

&#x20;                 Windows host

&#x20;            Splunk Enterprise

&#x20;         (SIEM + Detection Engine)

```



\---



\# Validation Checklist



| Component | Status |

| --- | --- |

| Kali Installed | ☐ |

| Ubuntu Installed | ☐ |

| Windows host | ☐ |

| Apache Running | ☐ |

| MariaDB Running | ☐ |

| PHP Working | ☐ |

| DVWA Working | ☐ |

| Splunk Running | ☐ |

| Universal Forwarder Running | ☐ |

| Logs Visible in Splunk | ☐ |



\---



\# Step 1: Verify IP Addresses



\## Kali



```bash

hostname -I

```



Example



```

192.168.70.139

```



\---



\## Ubuntu



```bash

hostname -I

```



Example



```

192.168.70.144

```



\---



\## Windows



```bash

ipconfig

```



Example



```

192.168.70.148

```



\---



\# Step 2: Verify Connectivity



\## From Kali



```bash

ping <Ubuntu-IP>

```



```bash

ping <Windows-IP>

```



Expected



```

0% packet loss

```



\---



\## From Ubuntu



```bash

ping <Kali-IP>



ping <Windows-IP>

```



\---



\## From Windows



```bash

ping <Ubuntu-IP>



ping <Kali-IP>

```



\---



\# Step 3: Verify SSH Access



From Kali



```bash

ssh <Ubuntu-Username>@<Ubuntu-IP>

```



Example



```bash

ssh adwithareddy@192.168.70.144

```



Login successfully.



Exit



```bash

exit

```



\---



\# Step 4: Verify Apache



Open Firefox in Kali.



Visit



```

http://<Ubuntu-IP>

```



Expected



```

Apache2 Ubuntu Default Page

```



\---



\# Step 5: Verify DVWA



Open



```

http://<Ubuntu-IP>/DVWA

```



Login



```

Username



admin



Password



password

```



Security Level



```

Low

```



\---



\# Step 6: Generate SSH Events



Attempt two successful SSH logins.



```bash

ssh adwithareddy@<Ubuntu-IP>

```



Exit



```bash

exit

```



\---



\# Step 7: Generate Apache Access Logs



Refresh the DVWA page multiple times.



Expected



Apache Access Logs Generated



\---



\# Step 8: Generate Failed Requests



Open



```

http://<Ubuntu-IP>/invalidpage

```



Expected



404 Error



Apache Error Log Generated



\---



\# Step 9: Generate Custom Syslog Event



On Ubuntu



```bash

logger "SOC Lab Validation Event"

```



\---



\# Step 10: Verify Splunk



Open



```

<http://localhost:8000>

```



Login



```

admin

```



Search



```

index=\*

```



Verify



\- SSH Events

\- Apache Access Events

\- Apache Error Events

\- Syslog Events



\---



\# Step 11: Verify Event Count



```

index=\* | stats count

```



Events should increase as new activity is generated.



\---



\# Step 12: Verify Host Names



```

index=\* | stats count by host

```



Expected Hosts



\- Ubuntu

\- Windows Server



\---



\# Step 13: Verify Log Sources



```

index=\* | stats count by source

```



Expected Sources



\- auth.log

\- access.log

\- error.log

\- syslog



\---



\# Step 14: Verify Sourcetypes



```

index=\* | stats count by sourcetype

```



Expected



Multiple sourcetypes displayed.



\---



\# Expected Result



The SOC Lab environment should now be fully operational.



The following components must work correctly:



\- Kali can reach Ubuntu.

\- Ubuntu can reach Splunk.

\- Splunk receives logs.

\- DVWA is accessible.

\- Apache generates logs.

\- SSH generates logs.

\- Searches return live events.



\---



\# Final Verification Checklist



\## Infrastructure



\- \[ ]  Kali Operational

\- \[ ]  Ubuntu Operational

\- \[ ]  Windows  Operational



\## Services



\- \[ ]  Apache Running

\- \[ ]  MariaDB Running

\- \[ ]  PHP Working

\- \[ ]  DVWA Accessible

\- \[ ]  SSH Running



\## Splunk



\- \[ ]  Enterprise Installed

\- \[ ]  Web Interface Accessible

\- \[ ]  Receiving Port Enabled

\- \[ ]  Universal Forwarder Connected

\- \[ ]  Events Searchable



\## Logging



\- \[ ]  SSH Logs

\- \[ ]  Apache Access Logs

\- \[ ]  Apache Error Logs

\- \[ ]  Syslog

\- \[ ]  Live Events



\---



\# Quick Validation Commands



\## Ubuntu



```bash

hostname -I



systemctl status apache2



systemctl status mariadb



systemctl status ssh



logger "SOC Lab Validation"



tail -5 /var/log/auth.log



tail -5 /var/log/apache2/access.log

```



\---



\## Kali



```bash

ping <Ubuntu-IP>



ssh <Ubuntu-Username>@<Ubuntu-IP>



nmap <Ubuntu-IP>

```



\---



\## Windows



```bash

ipconfig



sc query splunkd



netstat -ano | findstr 9997

```



\---



\## Splunk



```

index=\*



index=\* | stats count



index=\* | stats count by host



index=\* | stats count by source



index=\* | stats count by sourcetype

```



\---



\# Learning Outcome



After completing this page, you will be able to:



\- Verify the complete SOC lab environment.

\- Confirm end-to-end log collection.

\- Validate communication between all systems.

\- Ensure Splunk is ready for detection engineering.



\---

