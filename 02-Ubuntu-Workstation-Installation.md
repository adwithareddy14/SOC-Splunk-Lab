02 . Ubuntu Desktop Installation



\# Objective



\---



Install Ubuntu Desktop 24.04 LTS in VMware Workstation and configure it as the victim machine for the SOC lab.



Ubuntu will be used for:



\- Hosting the vulnerable web application (DVWA)

\- Running the Apache web server

\- Running the OpenSSH server

\- Generating logs for Splunk

\- Simulating attacks from Kali Linux



\---



\# Prerequisites



Before starting, ensure the following:



\- VMware Workstation 17 Pro is installed.

\- Ubuntu Desktop 24.04 LTS ISO is downloaded.

\- Virtualization (VT-x/AMD-V) is enabled in BIOS.

\- At least 40 GB of free disk space is available.

\- Minimum 16 GB RAM on the host machine.



\---



\# VM Configuration



| Setting | Value |

| --- | --- |

| Name | Ubuntu |

| Version | Ubuntu Desktop 24.04.4 LTS |

| RAM | 4096 MB (4 GB) |

| Processor | 2 Cores |

| Hard Disk | 40 GB |

| Disk Type | NVMe |

| Network Adapter | NAT |

| Firmware | UEFI |



\---



\# Step 1: Create a New Virtual Machine



1\. Open VMware Workstation.

2\. Click \*\*Create a New Virtual Machine\*\*.

3\. Select \*\*Typical (Recommended)\*\*.

4\. Click \*\*Next\*\*.



\*Create a New Virtual Machine Wizard\*



!image.png



\---



\# Step 2: Select Ubuntu ISO



1\. Select \*\*Installer disc image file (ISO)\*\*.

2\. Browse and select the Ubuntu Desktop 24.04.4 LTS ISO.

3\. Click \*\*Next\*\*.



\*Ubuntu ISO Selection\*



!image.png



\---



\# Step 3: Name the Virtual Machine



VM Name:



```

Ubuntu

```



Choose a suitable storage location.



Example:



```

D:\\Virtual Machines\\Ubuntu

```



Click \*\*Next\*\*.



\---



\# Step 4: Configure Disk



Virtual Disk Size



```

40 GB

```



Select:



```

Store virtual disk as a single file

```



Click \*\*Next\*\*.



\*Disk Configuration\*



!image.png



\---



\# Step 5: Customize Hardware



Click \*\*Customize Hardware\*\*.



Configure the following:



| Hardware | Value |

| --- | --- |

| Memory | 4096 MB |

| Processors | 2 |

| CD/DVD | Ubuntu ISO |

| Network Adapter | NAT |

| USB Controller | Default |

| Sound Card | Default |

| Display | Accelerate 3D Graphics Enabled |



Click \*\*Close\*\*.



Then click \*\*Finish\*\*.



\*VM Hardware Settings\*



!image.png



\---



\# Step 6: Power On the Virtual Machine



Click:



```

Power on this virtual machine

```



Ubuntu Installer will start.



\---



\# Step 7: Select Language



Choose



```

English

```



Click



```

Next

```



\---



\# Step 8: Keyboard Layout



Select



```

English (US)

```



Click



```

Next

```



\---



\# Step 9: Connect to Network



Ensure the VM is connected to the internet.



Click



```

Next

```



\---



\# Step 10: Installation Type



Choose



```

Interactive Installation

```



Click



```

Next

```



\---



\# Step 11: Applications



Select



```

Default Selection

```



Click



```

Next

```



\---



\# Step 12: Third-Party Software



Enable



\- Install third-party software for graphics and Wi-Fi hardware.



Click



```

Next

```



\---



\# Step 13: Disk Setup



Select



```

Erase disk and install Ubuntu

```



⚠️ This erases only the \*\*virtual disk\*\*, not your physical computer.



Click



```

Next

```



\---



\# Step 14: Time Zone



Select your location.



Example:



```

Asia/Kolkata

```



Click



```

Next

```



\---



\# Step 15: Create User



Example configuration



| Field | Value |

| --- | --- |

| Your Name | Adwitha Reddy |

| Computer Name | UBUNTU-WEB |

| Username | adwithareddy |

| Password | \*\*\*\*\*\*\*\* |



Enable



```

Require my password to log in

```



Click



```

Next

```



\---



\# Step 16: Install Ubuntu



Click



```

Install

```



Wait approximately 10–20 minutes.



\---



\# Step 17: Restart



After installation completes



Click



```

Restart Now

```



Remove the ISO if prompted.



Press



```

Enter

```



\---



\# Step 18: Login



Login using the username and password created earlier.



Ubuntu Desktop should now load successfully.



\---



\# Verification



Open Terminal and execute:



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



Verify Internet Connectivity



```bash

ping -c 4 google.com

```



Verify IP Address



```bash

hostname -I

```



\---



\# Expected Result



The Ubuntu virtual machine should:



\- Boot successfully.

\- Connect to the internet.

\- Obtain an IP address.

\- Access external websites.

\- Be ready for software installation.



\---



\# Checklist



\- \[ ]  Ubuntu Installed

\- \[ ]  Internet Working

\- \[ ]  Terminal Working

\- \[ ]  IP Address Assigned

\- \[ ]  Ready for Apache Installation



\---



\#

