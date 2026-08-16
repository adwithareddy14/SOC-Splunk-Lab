\# 📡 Page 09: Installing \& Configuring Splunk Universal Forwarder (Ubuntu)



\---



\# Objective



Install and configure Splunk Universal Forwarder on Ubuntu Desktop to securely forward system and application logs to Splunk Enterprise running on Windows Server 2019.



After completing this page:



\- Ubuntu will send logs to Splunk.

\- Splunk will index the received logs.

\- Log forwarding will be verified.



\---



\# Lab Architecture



```



```



```

&#x20;         Kali Linux

&#x20;        (Attacker)

&#x20;             │

&#x20;             ▼

&#x20;     Ubuntu Desktop

&#x20;(Victim + Universal Forwarder)

&#x20;             │

&#x20;    TCP Port 9997

&#x20;             │

&#x20;             ▼

&#x20; Windows Server 2019

&#x20;  Splunk Enterprise

```



```



\---



\# Prerequisites



\- Ubuntu Desktop installed

\- Splunk Enterprise running

\- Receiving Port 9997 configured

\- Ubuntu and Windows Server can ping each other



\---



\# Step 1: Verify Network Connectivity



Find the Windows IP.



Example

```



192.168.70.148



```



From Ubuntu



```bash

ping 192.168.70.148

```



Expected



```

0% packet loss

```



\---



\# Step 2: Download Splunk Universal Forwarder



Open Firefox.



Visit



```

<https://www.splunk.com>

```



Navigate to



```

Downloads



↓



Universal Forwarder

```



Download



```

Linux (.deb)

64-bit

```



\---



\# Step 3: Install the Universal Forwarder



Navigate to the Downloads folder.



```bash

cd \~/Downloads

```



Verify the package.



```bash

ls

```



Example



```

splunkforwarder-<version>-linux-amd64.deb

```



Install



```bash

sudo dpkg -i splunkforwarder-\*.deb

```



If dependencies are missing



```bash

sudo apt --fix-broken install -y

```



\---



\# Step 4: Verify Installation



```bash

ls /opt

```



Expected



```

splunkforwarder

```



\---



\# Step 5: Start Universal Forwarder



```bash

sudo /opt/splunkforwarder/bin/splunk start

```



Accept the license.



Type



```

y

```



Create credentials



Username



```

admin

```



Password



```

SplunkUF@123

```



\---



\# Step 6: Enable Boot Start



```bash

sudo /opt/splunkforwarder/bin/splunk enable boot-start

```



Expected



```

Boot-start enabled successfully.

```



\---



\# Step 7: Configure Deployment Server (Optional)



Skip for this lab.



\---



\# Step 8: Configure Forward Server



Example



```

Windows



192.168.70.148

```



Execute



```bash

sudo /opt/splunkforwarder/bin/splunk add forward-server 192.168.70.148:9997

```



Expected



```

Forward-server added successfully.

```



\---



\# Step 9: Configure Logs to Monitor



Monitor Apache logs



```bash

sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/apache2/access.log

```



Monitor Apache error logs



```bash

sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/apache2/error.log

```



Monitor SSH logs



```bash

sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/auth.log

```



Monitor Syslog



```bash

sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/syslog

```



\---



\# Step 10: Restart Universal Forwarder



```bash

sudo /opt/splunkforwarder/bin/splunk restart

```



\---



\# Step 11: Verify Forwarder Status



```bash

sudo /opt/splunkforwarder/bin/splunk list forward-server

```



Expected



```

Active

```



\---



\# Step 12: Verify Listening Connection



```bash

sudo ss -tnp

```



Expected



```

Connection established to



192.168.70.148:9997

```



\---



\# Step 13: Verify Logs in Splunk



Open Splunk.



Navigate



```

Search \& Reporting

```



Run



```

index=soc\_lab

```



If no index was created



```

index=\*

```



Expected



```

Ubuntu logs appear.

```



\---



\# Frequently Forwarded Logs



| Log File | Purpose |

| --- | --- |

| /var/log/auth.log | SSH Login Attempts |

| /var/log/apache2/access.log | Web Requests |

| /var/log/apache2/error.log | Apache Errors |

| /var/log/syslog | System Events |



\---



\# Expected Result



Ubuntu should now



\- Forward logs automatically.

\- Maintain a persistent connection to Splunk.

\- Send Apache logs.

\- Send SSH logs.

\- Send Syslog events.



\---



\# Verification Checklist



\- \[ ]  Universal Forwarder Installed

\- \[ ]  Forwarder Started

\- \[ ]  Boot Start Enabled

\- \[ ]  Forward Server Configured

\- \[ ]  Apache Logs Monitored

\- \[ ]  SSH Logs Monitored

\- \[ ]  Syslog Monitored

\- \[ ]  Logs Visible in Splunk



\---



\# Commands Summary



```bash

cd \~/Downloads



sudo dpkg -i splunkforwarder-\*.deb



sudo apt --fix-broken install -y



sudo /opt/splunkforwarder/bin/splunk start



sudo /opt/splunkforwarder/bin/splunk enable boot-start



sudo /opt/splunkforwarder/bin/splunk add forward-server 192.168.70.148:9997



sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/apache2/access.log



sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/apache2/error.log



sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/auth.log



sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/syslog



sudo /opt/splunkforwarder/bin/splunk restart



sudo /opt/splunkforwarder/bin/splunk list forward-server

```



\---



\# Troubleshooting



\## Universal Forwarder Not Starting



```bash

sudo /opt/splunkforwarder/bin/splunk status

```



Start manually



```bash

sudo /opt/splunkforwarder/bin/splunk start

```



\---



\## Cannot Connect to Splunk



Verify



```bash

ping <Windows\_Server\_IP>

```



Verify port 9997



```bash

netstat -ano | findstr 9997

```



\---



\## Logs Not Appearing



Restart the Universal Forwarder



```bash

sudo /opt/splunkforwarder/bin/splunk restart

```



Verify monitored inputs



```bash

sudo /opt/splunkforwarder/bin/splunk list monitor

```



\---



\# (or)



If not working follow this below :



click here below .



\# SPLUNK UNIVERSAL FORWARDER - UBUNTU → WINDOWS



\# Ubuntu IP: 192.168.111.128



\# Windows IP: 192.168.111.1



\# Splunk Port: 9997



\# 1. CHECK UBUNTU IP



hostname -I



\# Expected: 192.168.111.128



\# If incorrect:



ip addr

ip route



\# 2. TEST UBUNTU → WINDOWS



ping -c 4 192.168.111.1



\# Expected:



\# 4 packets transmitted, 4 received, 0% packet loss



\# If failed:



\# Check Windows:



\# ipconfig



\# Confirm VMnet8 = 192.168.111.1



\# Check VMware Ubuntu Network Adapter = NAT/VMnet8



\# 3. GO TO DOWNLOADS



cd \~/Downloads

ls



\# Expected:



\# splunkforwarder-<version>-linux-amd64.deb



\# If package not found:



find \~ -name "splunkforwarder\*.deb" 2>/dev/null



\# 4. INSTALL FORWARDER



sudo dpkg -i splunkforwarder-\*.deb



\# Expected:



\# Setting up splunkforwarder (...)



\# complete



\# If dependency error:



sudo apt --fix-broken install -y

sudo dpkg -i splunkforwarder-\*.deb



\# 5. VERIFY INSTALLATION



sudo /opt/splunkforwarder/bin/splunk version



\# Expected:



\# Splunk Universal Forwarder 10.x.x



\# If not found:



ls /opt



\# Expected:



\# splunkforwarder



\# 6. START FORWARDER



sudo /opt/splunkforwarder/bin/splunk start



\# Expected:



\# Starting splunkd...



\# Done



\# If failed:



sudo /opt/splunkforwarder/bin/splunk status

sudo tail -50 /opt/splunkforwarder/var/log/splunk/splunkd.log



\# 7. CHECK STATUS



sudo /opt/splunkforwarder/bin/splunk status



\# Expected:



\# splunkd is running



\# If not running:



sudo /opt/splunkforwarder/bin/splunk start



\# 8. ENABLE BOOT START



sudo /opt/splunkforwarder/bin/splunk enable boot-start



\# Expected:



\# Boot-start enabled successfully.



\# 9. WINDOWS SPLUNK RECEIVER



\# On Windows Splunk:



\# Settings



\# → Forwarding and Receiving



\# → Configure Receiving



\# → Add New



\# → Port: 9997



\# → Save



\# 10. WINDOWS CHECK PORT



\# Run Windows CMD as Administrator:



netstat -ano | findstr :9997



\# Expected:



\# TCP 0.0.0.0:9997 0.0.0.0:0 LISTENING <PID>



\# If nothing appears:



\# Check Splunk receiving port 9997.



\# Restart Splunk Enterprise if necessary.



\# 11. WINDOWS FIREWALL CHECK



\# Run Windows PowerShell as Administrator:



Get-NetFirewallProfile | Select-Object Name,Enabled



\# Expected:



\# Domain/Private/Public profiles shown



\# Check 9997 rule:



Get-NetFirewallRule -Enabled True | Where-Object {$\*.Direction -eq "Inbound"} | Get-NetFirewallPortFilter | Where-Object {$\*.Protocol -eq "TCP" -and $\_.LocalPort -eq "9997"}



\# 12. WINDOWS FIREWALL - ALLOW 9997



\# Only run if TCP 9997 is blocked:



New-NetFirewallRule -DisplayName "Splunk Receiving TCP 9997" -Direction Inbound -Protocol TCP -LocalPort 9997 -Action Allow



\# Expected:



\# Enabled: True



\# Direction: Inbound



\# Action: Allow



\# 13. OPTIONAL - RESTRICT FIREWALL TO UBUNTU



Remove-NetFirewallRule -DisplayName "Splunk Receiving TCP 9997"



New-NetFirewallRule -DisplayName "Splunk UF Ubuntu 9997" -Direction Inbound -Protocol TCP -LocalPort 9997 -RemoteAddress 192.168.111.128 -Action Allow



\# 14. UBUNTU CHECK UFW



sudo ufw status verbose



\# If:



\# Status: inactive



\# No UFW action required.



\# If UFW is active:



\# Normally outbound connections are allowed.



\# Verify:



sudo ufw status verbose



\# 15. TEST TCP 9997 FROM UBUNTU



nc -vz 192.168.111.1 9997



\# Expected:



\# Connection to 192.168.111.1 9997 port \[tcp/\*] succeeded!



\# If nc is missing:



sudo apt install netcat-openbsd -y

nc -vz 192.168.111.1 9997



\# If failed:



\# "Connection refused" = Windows/Splunk is not accepting 9997.



\# "Timed out" = firewall/network issue.



\# Check Windows:



\# netstat -ano | findstr :9997



\# 16. ADD WINDOWS SPLUNK FORWARD SERVER



sudo /opt/splunkforwarder/bin/splunk add forward-server 192.168.111.1:9997



\# Expected:



\# Added forwarding to: 192.168.111.1:9997



\# 17. VERIFY FORWARD SERVER



sudo /opt/splunkforwarder/bin/splunk list forward-server



\# Expected:



\# 192.168.111.1:9997



\# Active



\# If not Active:



nc -vz 192.168.111.1 9997

sudo /opt/splunkforwarder/bin/splunk restart

sudo /opt/splunkforwarder/bin/splunk list forward-server



\# 18. MONITOR SSH LOG



sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/auth.log



\# Expected:



\# Added monitor of /var/log/auth.log



\# If missing:



ls -l /var/log/auth.log



\# 19. MONITOR SYSLOG



sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/syslog



\# Expected:



\# Added monitor of /var/log/syslog



\# If missing:



ls -l /var/log/syslog



\# 20. OPTIONAL APACHE ACCESS LOG



sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/apache2/access.log



\# If missing:



ls -l /var/log/apache2/

sudo systemctl status apache2



\# 21. OPTIONAL APACHE ERROR LOG



sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/apache2/error.log



\# 22. CHECK MONITORS



sudo /opt/splunkforwarder/bin/splunk list monitor



\# Expected:



\# /var/log/auth.log



\# /var/log/syslog



\# Optional:



\# /var/log/apache2/access.log



\# /var/log/apache2/error.log



\# 23. RESTART FORWARDER



sudo /opt/splunkforwarder/bin/splunk restart



\# Expected:



\# Stopping splunkd...



\# Starting splunkd...



\# Done



\# 24. FINAL STATUS



sudo /opt/splunkforwarder/bin/splunk status



\# Expected:



\# splunkd is running



sudo /opt/splunkforwarder/bin/splunk list forward-server



\# Expected:



\# 192.168.111.1:9997



\# Active



sudo /opt/splunkforwarder/bin/splunk list monitor



\# Expected:



\# /var/log/auth.log



\# /var/log/syslog



\# 25. GENERATE TEST LOG



logger "SPLUNK\_TEST Ubuntu Forwarding Working"



\# 26. VERIFY TEST LOG LOCALLY



grep "SPLUNK\_TEST" /var/log/syslog



\# Expected:



\# ... SPLUNK\_TEST Ubuntu Forwarding Working



\# 27. SEARCH WINDOWS SPLUNK



\# Splunk → Search \& Reporting



\# Search:



\# "SPLUNK\_TEST"



\# 



\# Or:



\# index=\* "SPLUNK\_TEST"



\# Expected:



\# SPLUNK\_TEST Ubuntu Forwarding Working



\# 28. IF LOG IS NOT VISIBLE IN SPLUNK



sudo /opt/splunkforwarder/bin/splunk status

sudo /opt/splunkforwarder/bin/splunk list forward-server

sudo /opt/splunkforwarder/bin/splunk list monitor

nc -vz 192.168.111.1 9997



\# Windows:



netstat -ano | findstr :9997



\# Check Windows Firewall:



Get-NetFirewallRule -DisplayName "\*9997\*" | Format-Table DisplayName,Enabled,Direction,Action



\# Generate another test:



logger "SPLUNK\_FINAL\_TEST"



\# Search in Windows Splunk:



\# "SPLUNK\_FINAL\_TEST"



\# FINAL WORKING STATE:



\# Ubuntu 192.168.111.128



\# |



\# | TCP 9997



\# v



\# Windows 192.168.111.1



\# |



\# v



\# Splunk Enterprise



\# 



\# Forwarder = RUNNING



\# Receiver = 9997 LISTENING



\# Firewall = TCP 9997 ALLOWED



\# Forward Server = ACTIVE



\# Logs = VISIBLE



\# ============================================================



\# FIREWALL TROUBLESHOOTING



\# Ubuntu → Windows Splunk



\# Ubuntu IP : 192.168.111.128



\# Windows IP : 192.168.111.1



\# Splunk : TCP 9997



\# ============================================================



\# ============================================================



\# 1. WINDOWS — CHECK WHETHER PORT 9997 IS LISTENING



\# ============================================================



\# Run on WINDOWS CMD as Administrator:



netstat -ano | findstr :9997



\# EXPECTED:



\# TCP 0.0.0.0:9997 0.0.0.0:0 LISTENING <PID



\# If you see LISTENING:



\# Splunk is listening on TCP 9997.



\# ============================================================



\# 2. WINDOWS — CHECK WINDOWS FIREWALL



\# ============================================================



\# Run PowerShell as Administrator:



Get-NetFirewallProfile | Select-Object Name, Enabled



\# Example:



\# Name Enabled



\# --- -------



\# Domain True



\# Private True



\# Public True



\# ============================================================



\# 3. WINDOWS — CHECK WHETHER A 9997 FIREWALL RULE EXISTS



\# ============================================================



Get-NetFirewallRule -Enabled True |

Where-Object {$\*.Direction -eq "Inbound"} |

Get-NetFirewallPortFilter |

Where-Object {$\*.Protocol -eq "TCP" -and $\_.LocalPort -eq "9997"}



\# EXPECTED:



\# A rule associated with TCP 9997



\# If nothing is returned, there may be no inbound firewall



\# rule allowing TCP 9997.



\# ============================================================



\# 4. WINDOWS — CREATE FIREWALL RULE FOR SPLUNK 9997



\# ============================================================



\# ONLY RUN THIS IF TCP 9997 IS BLOCKED.



\# Run PowerShell as Administrator



New-NetFirewallRule     `-DisplayName "Splunk Receiving TCP 9997"`

\-Direction Inbound     `-Protocol TCP`

\-LocalPort 9997 `

\-Action Allow



\# EXPECTED:



\# Name : ...



\# DisplayName : Splunk Receiving TCP 9997



\# Enabled : True



\# Direction : Inbound



\# Action : Allow



\# ============================================================



\# 5. WINDOWS — VERIFY THE NEW RULE



\# ============================================================



Get-NetFirewallRule -DisplayName "Splunk Receiving TCP 9997"



\# EXPECTED:



\# Enabled : True



\# Direction : Inbound



\# Action : Allow



\# ============================================================



\# 6. WINDOWS — MORE RESTRICTED RULE



\# ============================================================



\# OPTIONAL:



\# Instead of allowing TCP 9997 from every source, restrict it



\# to your Ubuntu IP.



\# Remove the broad rule first if you created it:



Remove-NetFirewallRule -DisplayName "Splunk Receiving TCP 9997"



\# Then create a rule allowing only Ubuntu:



New-NetFirewallRule     `-DisplayName "Splunk UF Ubuntu 9997"`

\-Direction Inbound     `-Protocol TCP`

\-LocalPort 9997     `-RemoteAddress 192.168.111.128`

\-Action Allow



\# EXPECTED:



\# Ubuntu 192.168.111.12



\# | TCP 9997 ALLOWE



\# Windows 192.168.111.1



\# ============================================================



\# 7. UBUNTU — CHECK UFW STATUS



\# ============================================================



\# Run on Ubuntu:



sudo ufw status verbose



\# POSSIBLE OUTPUT



\# Status: inactive



\# If UFW is inactive:



\# Ubuntu is not blocking traffic with UFW.



\# ============================================================



\# 8. UBUNTU — IF UFW IS ACTIVE



\# ============================================================



sudo ufw status



\# Example



\# Status: active



\# ============================================================



\# 9. UBUNTU — IMPORTANT



\# ============================================================



\# The Splunk connection is OUTBOUND:



\# Ubuntu → Windows:9997



\# Therefore, normally you do NOT need to open inbound TCP



\# 9997 on Ubuntu.



\# If UFW has restrictive outbound rules, check:



sudo ufw status verbose



\# Look for:



\# Default: deny (incoming), allow (outgoing)



\# This is normally fine.



\# ============================================================



\# 10. UBUNTU — TEST TCP 9997



\# ============================================================



nc -vz 192.168.111.1 9997



\# WORKING:



\# Connection to 192.168.111.1 9997 port \[tcp/\*] succeeded!



\# ============================================================



\# 11. IF TCP CONNECTION FAILS



\# ============================================================



\# Example:



\# nc: connect to 192.168.111.1 port 9997 failed:



\# Connection refused



\# Check Windows:



netstat -ano | findstr :9997



\# If there is NO LISTENING:



\# Splunk Enterprise is not listening on 9997



\# Go to:



\# Splunk



\# → Settings



\# → Forwarding and Receiving



\# → Configure Receiving



\# → Add New



\# → 9997



\# → Save



\# ============================================================



\# 12. IF WINDOWS SHOWS LISTENING BUT UBUNTU CANNOT CONNECT



\# ============================================================



\# Check Windows Firewall rule:



Get-NetFirewallRule -DisplayName "\*9997\*" |

Format-Table DisplayName, Enabled, Direction, Action



\# EXPECTED:



\# Enabled : True



\# Direction : Inbound



\# Action : Allow



\# Then test again from Ubuntu:



nc -vz 192.168.111.1 9997



\# ============================================================



\# 13. IF WINDOWS FIREWALL IS THE PROBLEM



\# ============================================================



\# Create the restricted rule



New-NetFirewallRule     `-DisplayName "Splunk UF Ubuntu 9997"`

\-Direction Inbound     `-Protocol TCP`

\-LocalPort 9997     `-RemoteAddress 192.168.111.128`

\-Action Allow



\# Then from Ubuntu



nc -vz 192.168.111.1 9997



\# EXPECTED:



\# succeeded



\# ============================================================



\# 14. AFTER FIREWALL IS FIXED — CHECK SPLUNK



\# ============================================================



\# Ubuntu:



sudo /opt/splunkforwarder/bin/splunk list forward-server



\# EXPECTED:



\# 192.168.111.1:9997



\# Active



\# ============================================================



\# 15. GENERATE TEST LOG



\# ============================================================



logger "SPLUNK\_FIREWALL\_TEST"



\# Then search in Windows Splunk:



\# "SPLUNK\_FIREWALL\_TEST"



\# EXPECTED:



\# Ubuntu event appears in Splunk.



\# ============================================================



\# QUICK TROUBLESHOOTING ORDER



\# ============================================================



\# If logs are NOT appearing, check in this exact order:



\# 1. Ubuntu → Windows IP:



ping -c 4 192.168.111.1



\# Expected:



\# 0% packet los



\# 2. Windows Splunk receiving:



\# Windows CMD:



netstat -ano | findstr :999



\# Expected:



\# LISTENIN



\# 3. Windows Firewall:



\# Windows PowerShell:



Get-NetFirewallRule -DisplayName "\*9997\*" |

Format-Table DisplayName, Enabled, Direction, Action



\# Enabled=True



\# Direction=Inbound



\# Action=Allow



\# 4. Ubuntu → Windows TCP:



nc -vz 192.168.111.1 9997



\# Expected:



\# succeeded



\# 5. Splunk Forwarder:



sudo /opt/splunkforwarder/bin/splunk status



\# Expected:



\# splunkd is running



\# 6. Forward server:



sudo /opt/splunkforwarder/bin/splunk list forward-server



\# Expected:



\# 192.168.111.1:9997



\# Active



\# 7. Monitors:



sudo /opt/splunkforwarder/bin/splunk list monitor



\# Expected:



\# /var/log/auth.log



\# /var/log/syslog



\# 8. Test:



logger "SPLUNK\_FINAL\_TEST"



\# Search Windows Splunk:



\# "SPLUNK\_FINAL\_TEST"



\# ============================================================



\# FINAL WORKING STATE



\# ============================================================



\# Ubuntu



\# 192.168.111.128



\# |



\# | TCP 9997



\# | Windows Firewall: ALLOW



\# v



\# Windows



\# 192.168.111.1



\# |



\# v



\# Splunk Enterprise



\# Forwarder: RUNNING



\# Receiver: 9997 LISTENING



\# Firewall: TCP 9997 ALLOWED



\# Forward Server: ACTIVE



\# Logs: VISIBLE IN SPLUNK



\# ============================================================



Learning Outcome :



After completing this page, you will be able to:



\- Install Splunk Universal Forwarder.

\- Configure a forward server.

\- Monitor Linux log files.

\- Forward logs to Splunk Enterprise.

\- Verify successful log ingestion.



\---



\#

