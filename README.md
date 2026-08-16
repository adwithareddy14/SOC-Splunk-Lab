\# SIEM-Based Cyber Attack Detection using Splunk



\## Overview



This project demonstrates Security Information and Event Management (SIEM) using Splunk to detect and generate alerts for simulated cyber attacks.



The lab environment uses Kali Linux as the attacker, Ubuntu as the victim/server, and Splunk Enterprise as the SIEM platform.



Logs generated on the victim system are collected using Splunk Universal Forwarder and sent to Splunk Enterprise for analysis. Splunk detection rules identify suspicious activities and generate alerts for investigation.



\## Lab Architecture



```text

Kali Linux

(Attacker)

&#x20;    |

&#x20;    | Simulated attacks

&#x20;    ↓

Ubuntu

(Victim / Server)

&#x20;    |

&#x20;    | Logs

&#x20;    ↓

Splunk Universal Forwarder

&#x20;    |

&#x20;    | Forwarded logs

&#x20;    ↓

Splunk Enterprise

(SIEM)

&#x20;    |

&#x20;    | Detection Rules

&#x20;    ↓

Alerts

&#x20;    |

&#x20;    ↓

SOC Investigation

