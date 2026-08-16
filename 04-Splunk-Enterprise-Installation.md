\# Page 04: Shared Folder Configuration \& Splunk Enterprise Installation



\---



\# Objective



Configure a VMware Shared Folder to simplify file sharing between the host machine and virtual machines. Use the shared folder to install Splunk Enterprise on Windows Server 2019.



This approach avoids downloading software directly inside the virtual machine and provides a centralized repository for all lab software.



\---



\# Why Use a Shared Folder?



Instead of downloading software separately in each virtual machine:



Host Computer

↓



Shared Folder

↓



Windows 



↓



Ubuntu



Benefits:



\- Faster software installation.

\- No dependency on Internet Explorer.

\- Easy software management.

\- Reusable for future labs.

\- Recommended for workshop environments.



\---



\# Folder Structure on Host Machine



Create the following directory on the Windows host.



Example



```

D:\\SOC\_Lab

```



Inside it create:



```

SOC\_Lab

│

├── Downloads

├── ISOs

├── Scripts

├── Tools

├── Logs

└── Documentation

```



Recommended Downloads folder



```

D:\\SOC\_Lab\\Downloads

```



Store the following software inside this folder.



| Software | Purpose |

| --- | --- |

| Splunk Enterprise (.msi) | SIEM Platform |

| Google Chrome Enterprise (.msi) | Web Browser |

| Splunk Universal Forwarder | Log Collection |

| DVWA.zip | Vulnerable Web Application |



\---



\# Step 1: Download Required Software



Download on the Host Machine (Windows 11).



Required software



\- Splunk Enterprise (Windows 64-bit MSI)

\- Google Chrome Enterprise MSI



Verify that the downloaded files are available in



```

D:\\SOC\_Lab\\Downloads

```



\---



\# Step 2: Enable VMware Shared Folder



Power OFF the Windows Sevirtual machine.



Open VMware Workstation.



Right-click



```

Windows 

```



Select



```

Settings

```



Navigate to



```

Options

→ Shared Folders

```



Select



```

Always Enabled

```



Click



```

Add...

```



\---



\# Step 3: Add Shared Folder



Browse to



```

D:\\SOC\_Lab

```



Folder Name



```

SOC\_Lab

```



Enable



```

Read-only → Disabled



Enable this share

```



Click



```

Finish

```



( not in windows server 2019 , do it in host machine windows )



\---



\# Step 4: Start Windows



\---



\# Step 5: Access Shared Folder



Open File Explorer.



Navigate to



```

\\\\vmware-host\\Shared Folders\\

```



You should see



```

SOC\_Lab

```



Open



```

Downloads

```



Verify that the downloaded files are visible.



Example



```

Splunk-Enterprise.msi



GoogleChromeEnterprise.msi

```



📷 Screenshot:

\*Shared Folder in Windows Server\*



\---



\# Step 6: Install Google Chrome (Recommended)



Open Command Prompt as Administrator.



Navigate to



```bash

cd "\\\\vmware-host\\Shared Folders\\SOC\_Lab\\Downloads"

```



List available files



```bash

dir

```



Locate the Chrome installer.



Install Chrome



```bash

msiexec /i GoogleChromeEnterprise\*.msi

```



Complete the installation.



Verify Chrome launches successfully.



📷 Screenshot:

\*Google Chrome Installed\*



\---



\# Step 7: Install Splunk Enterprise



In Command Prompt



```bash

cd "\\\\vmware-host\\Shared Folders\\SOC\_Lab\\Downloads"

```



Locate the installer



```bash

dir

```



Install Splunk



```bash

msiexec /i Splunk\*.msi

```



Follow the installation wizard.



During installation



License



```

Accept

```



Installation Type



```

Local System

```



Administrator Username



```

admin

```



Administrator Password



```

\*\*\*\*\*\*\*\*

```



Click



```

Install

```



Wait for installation to complete.



\---



\# Step 8: Verify Splunk Service



Open Command Prompt



Execute



```bash

sc query splunkd

```



Expected Output



```

STATE : RUNNING

```



\---



\# Step 9: Verify Splunk Version



```bash

cd "C:\\Program Files\\Splunk\\bin"



splunk version

```



Expected Output



```

Splunk Enterprise



Version xx.x.x

```



\---



\# Step 10: Open Splunk



Launch Google Chrome.



Visit



```

<http://localhost:8000>

```



Login



Username



```

admin

```



Password



```

\*\*\*\*\*\*\*\*

```



Splunk Home Dashboard should appear.



\*Splunk Home Dashboard\*



!image.png



\---



\# Expected Result



At the end of this page



\- Shared Folder is configured.

\- Files are accessible from Windows

\- Google Chrome is installed.

\- Splunk Enterprise is installed.

\- Splunk service is running.

\- Splunk Web is accessible.



\---



\# Troubleshooting



\## Shared Folder Not Visible



Verify



\- VMware Tools is installed.

\- Shared Folder is enabled.

\- VM is powered off while configuring the share.

\- Folder path is correct.



\---



\## Splunk Service Not Running



Execute



```bash

cd "C:\\Program Files\\Splunk\\bin"



splunk start

```



\---



\## Verify Splunk Version



```bash

splunk version

```



\---



\# Checklist



\- \[ ]  Shared Folder Created

\- \[ ]  Shared Folder Accessible

\- \[ ]  Google Chrome Installed

\- \[ ]  Splunk Installed

\- \[ ]  Splunk Service Running

\- \[ ]  Splunk Login Successful



\# (Or)



if above commands are not working follow this below commands after downloading and installing 



!image.png



\# 



!image.png



!image.png



!image.png



!image.png



!image.png



\##

