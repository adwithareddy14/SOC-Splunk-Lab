\# 🐧 Page 05: Ubuntu Initial Configuration



\---



\# Objective



Perform the initial configuration of Ubuntu Desktop after installation to prepare it for hosting vulnerable applications and generating logs for Splunk.



\---



\# Prerequisites



\- Ubuntu Desktop 24.04.4 LTS installed

\- Internet connectivity available

\- User account created during installation

\- VMware Network Adapter configured as NAT



\---



\# Configuration Overview



| Item | Value |

| --- | --- |

| Hostname | ubuntu |

| Network | NAT |

| User | adwithareddy |

| SSH | Enabled |

| Updates | Latest |



\---



\# Step 1: Update Package Repository



Open Terminal.



Execute:



```bash

sudo apt update

```



Expected Result



```

Package lists updated successfully.

```



\---



\# Step 2: Upgrade Installed Packages



```bash

sudo apt upgrade -y

```



This may take several minutes.



\---



\# Step 3: Verify Ubuntu Version



```bash

lsb\_release -a

```



Expected Output



```

Distributor ID: Ubuntu

Description: Ubuntu 24.04.4 LTS

Release: 24.04

Codename: noble

```



\---



\# Step 4: Verify Internet Connectivity



```bash

ping -c 4 google.com

```



Expected Result



```

0% packet loss

```



\---



\# Step 5: Verify IP Address



```bash

hostname -I

```



Example



```

192.168.70.xxx

```



\---



\# Step 6: Verify Hostname



```bash

hostname

```



Expected Output



```

ubuntu

```



\---



\# Step 7: Install OpenSSH Server



```bash

sudo apt install openssh-server -y

```



\---



\# Step 8: Verify SSH Service



```bash

sudo systemctl status ssh

```



Expected Result



```

Active: active (running)

```



Press



```

q

```



to exit.



\---



\# Step 9: Enable SSH at Boot



```bash

sudo systemctl enable ssh

```



\---



\# Step 10: Verify Firewall Status



```bash

sudo ufw status

```



Expected Result



```

Status: inactive

```



If inactive, no action is required.



\---



\# Step 11: Verify Disk Space



```bash

df -h

```



Ensure sufficient free space is available.



\---



\# Step 12: Verify Memory



```bash

free -h

```



\---



\# Step 13: Verify Network Interface



```bash

ip addr

```



Locate the active network interface (typically `ens33`).



\---



\# Expected Result



Ubuntu should:



\- Be fully updated.

\- Have internet connectivity.

\- Have SSH running.

\- Have a valid IP address.

\- Be ready for Apache installation.



\---



\# Verification Checklist



\- \[ ]  Ubuntu updated

\- \[ ]  Packages upgraded

\- \[ ]  Internet working

\- \[ ]  SSH installed

\- \[ ]  SSH running

\- \[ ]  IP address verified

\- \[ ]  Hostname verified



\---



\# Commands Summary



```bash

sudo apt update



sudo apt upgrade -y



lsb\_release -a



hostname



hostname -I



ping -c 4 google.com



sudo apt install openssh-server -y



sudo systemctl status ssh



sudo systemctl enable ssh



sudo ufw status



df -h



free -h



ip addr

```



\---



\#

