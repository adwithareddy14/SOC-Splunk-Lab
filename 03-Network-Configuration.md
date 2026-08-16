03\. Network Configuration 



\# 🌐 Page 03: Virtual Network Configuration



\---



\# Objective



Configure all virtual machines to communicate with each other using VMware NAT networking.



This enables:



\- Kali Linux to attack Ubuntu.

\- Ubuntu to send logs to Splunk.

\- Windows to receive logs

\- All virtual machines to access the Internet.



\---



\# Network Topology



```



```



```

&#x20;            Internet

&#x20;                │

&#x20;     Windows 11 Host Machine

&#x20;                │

&#x20;     VMware NAT Network (VMnet8)

&#x20;                │

&#x20;┌───────────────┼───────────────┐

&#x20;│               │               │

&#x20;│               │               │

```



Kali Linux      Ubuntu Desktop   Windows 

(Attacker)      (Victim)         (Splunk Server)



```



\---



\# Network Mode



All virtual machines must use:

```



NAT



```



Do \*\*NOT\*\* use:



\- Host Only

\- Bridged



\---



\# Why NAT?



Advantages



\- Internet connectivity.

\- Communication between all VMs.

\- Safe isolated environment.

\- No impact on the college or home network.



\---



\# Step 1: Configure Kali



Power off the VM.



VMware

```



VM

→ Settings

→ Network Adapter



```



Select

```



NAT



```



Enable

```



Connected



Connect at power on



```



Save the settings.



\_Kali Network Adapter\_



\---



\# Step 2: Configure Ubuntu



Repeat the same process.



Network Adapter

```



NAT



```



Enable

```



Connected



Connect at power on



```



\_Ubuntu Network Adapter\_



\---



\# Step 3: Configure Windows 



Repeat the same process.



Network Adapter

```



NAT



```



Enable

```



Connected



Connect at power on



```



\_Windows Network Adapter\_



\---



\# Step 4: Verify IP Address



\## Kali



Open Terminal



```bash

hostname -I

```



Example



```

192.168.70.xxx

```



\---



\## Ubuntu



Open Terminal



```bash

hostname -I

```



Example



```

192.168.70.xxx

```



\---



\## Windows



Open Command Prompt



```bash

ipconfig

```



Example



```

IPv4 Address . . . . . : 192.168.70.xxx

```



\---



\# Step 5: Verify Connectivity



From Kali



```bash

ping <Ubuntu-IP>

```



Example



```bash

ping 192.168.70.144

```



Expected Result



```

0% packet loss

```



\---



From Ubuntu



```bash

ping <Windows-IP>

```



Expected Result



```

0% packet loss

```



\---



From Windows 



```bash

ping <Ubuntu-IP>



ping <Kali-IP>

```



Expected Result



```

Reply from...

```



\---



\# Step 6: Verify Internet



\## Kali



```bash

ping -c 4 google.com

```



\---



\## Ubuntu



```bash

ping -c 4 google.com

```



\---



\## Windows 



```bash

ping google.com

```



\---



\# Expected Result



All virtual machines should:



\- Receive an IPv4 address.

\- Communicate with each other.

\- Access the Internet.

\- Remain isolated from the physical network.



\---



\# Checklist



\- \[ ]  Kali connected

\- \[ ]  Ubuntu connected

\- \[ ]  Windows connected

\- \[ ]  Internet working

\- \[ ]  All VMs can ping each other



\---

