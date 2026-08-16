\# 📊 Page 08: Splunk Enterprise Installation \& Initial Configuration



\---



\# Objective



Install Splunk Enterprise on Windows ( Host machine ) and perform the initial configuration required for log collection and SIEM operations.



After completing this page, Splunk will be ready to receive logs from Ubuntu and Windows systems.



\---



\# Prerequisites



\- Windows Server 2019 installed

\- Google Chrome installed

\- Splunk Enterprise MSI downloaded

\- Administrator privileges



\---



\# Lab Architecture



```



```



```

&#x20;            Kali Linux

&#x20;                │

&#x20;   (Attack Traffic \& Logs)

&#x20;                │

&#x20;                ▼

&#x20;         Ubuntu Desktop

&#x20;  (Apache, SSH, DVWA Logs)

&#x20;                │

&#x20;        Universal Forwarder

&#x20;                │

&#x20;           Port 9997

&#x20;                │

&#x20;                ▼

&#x20;     Windows Server 2019

&#x20;        Splunk Enterprise

```



```



\---



\# Step 1: Install Splunk Enterprise



Locate

```



Splunk-<version>-x64-release.msi



```



Double-click the installer.



\---



\# Step 2: Accept License



Enable

```



I accept the License Agreement



```



Click

```



Next



```



\---



\# Step 3: Installation Type



Select

```



Local System



```



Click

```



Next



```



\---



\# Step 4: Create Splunk Administrator



Example



Username

```



admin



```



Password

```



Splunk@123



```



Click

```



Next



```



\---



\# Step 5: Install



Click

```



Install



```



Wait 5–10 minutes.



\---



\# Step 6: Verify Installation



Open Command Prompt.



```cmd

cd "C:\\Program Files\\Splunk\\bin"

```



Check version.



```bash

splunk version

```



Expected Output



```

Splunk Enterprise

Version: xx.x.x

```



\---



\# Step 7: Verify Splunk Service



```bash

sc query splunkd

```



Expected Output



```

STATE : RUNNING

```



\---



\# Step 8: Start Splunk (If Required)



```bash

cd "C:\\Program Files\\Splunk\\bin"



splunk start

```



Accept the license when prompted.



Expected



```

Splunk web server started.

```



\---



\# Step 9: Open Splunk



Launch Google Chrome.



Open



```

http://localhost:8000

```



Login



Username



```

admin

```



Password



```

password

```



\---



\# Step 10: Verify Splunk Home



Verify the following apps are visible.



\- Search \& Reporting

\- Dashboards

\- Alerts

\- Reports



📷 Screenshot



```

Splunk Home Dashboard

```



\---



\# Step 11: Enable Boot Start



Open Command Prompt as Administrator.



```bash

cd "C:\\Program Files\\Splunk\\bin"



splunk enable boot-start

```



Expected



```

Service enabled successfully.

```



\---



\# Step 12: Configure Receiving Port



Open Splunk.



Navigate



```

Settings



→ Forwarding and Receiving



→ Configure Receiving



→ New Receiving Port

```



Enter



```

9997

```



Click



```

Save

```



Expected



```

Port 9997 Enabled

```



📷 Screenshot



```

Receiving Port 9997

```



\---



\# Step 13: Create Index



Navigate



```

Settings



→ Indexes



→ New Index

```



Create



```

Index Name



soc\_lab

```



Retention



```

Default

```



Save.



\---



\# Step 14: Verify Listening Port



Open Command Prompt.



```bash

netstat -ano | findstr 9997

```



Expected



```

LISTENING

```



\---



\# Step 15: Verify Web Port



```bash

netstat -ano | findstr 8000

```



Expected



```

LISTENING

```



\---



\# Splunk Default Ports



| Service | Port |

| --- | --- |

| Splunk Web | 8000 |

| Management | 8089 |

| Forwarder | 9997 |



\---



\# Expected Result



Splunk should now



\- Be installed successfully.

\- Start automatically.

\- Open on port 8000.

\- Listen on port 9997.

\- Have a dedicated index named \*\*soc\_lab\*\*.



\---



\# Verification Checklist



\- \[ ]  Splunk Installed

\- \[ ]  Login Successful

\- \[ ]  Dashboard Accessible

\- \[ ]  Boot Start Enabled

\- \[ ]  Port 8000 Listening

\- \[ ]  Port 9997 Listening

\- \[ ]  soc\_lab Index Created



\---



\# Commands Summary



```bash

cd "C:\\Program Files\\Splunk\\bin"



splunk version



splunk start



splunk enable boot-start



sc query splunkd



netstat -ano | findstr 8000



netstat -ano | findstr 9997

```



\---



\# Troubleshooting



\### Splunk Service Not Running



```bash

sc query splunkd



cd "C:\\Program Files\\Splunk\\bin"



splunk start

```



\---



\### Port 8000 Not Listening



```bash

netstat -ano | findstr 8000

```



Restart Splunk



```bash

splunk restart

```



\---



\### Cannot Open Web Interface



Check Windows Firewall.



Verify



```

<http://localhost:8000>

```



or



```

<http://127.0.0.1:8000>

```



\---



\# Learning Outcome



After completing this page, you will be able to:



\- Install Splunk Enterprise.

\- Configure Splunk Web.

\- Enable automatic startup.

\- Configure a receiving port.

\- Create a dedicated index for SOC logs.

\- Verify that Splunk is ready to receive logs.



\---



\#

