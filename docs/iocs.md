# Indicators of Compromise (IOCs)

## Overview

This document lists the Indicators of Compromise (IOCs) identified during the SOC investigation.

| IOC Type | Value | Description |
|----------|-------|-------------|
| Victim Hostname | `DESKTOP-LAP0325` | Windows 11 victim machine |
| Attacker IP Address | `192.168.1.48` | Kali Linux attacker machine |
| Remote Service | RDP (TCP 3389) | Remote Desktop Protocol |
| Successful Logon | Event ID 4624 | Successful RDP authentication |
| Failed Logons | Event ID 4625 | Brute-force login attempts |
| Payload Name | `persistence.exe` | Malicious executable |
| Payload Location | `C:\Users\victim\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\` | Startup folder used for persistence |
| Process Creation | Event ID 1 | Payload execution detected |
| File Creation | Event ID 11 | Payload file creation detected |
| Network Connection | Event ID 3 | Reverse shell connection |
| Destination Port | 4444 | Netcat listener port |
| SIEM Platform | Splunk Enterprise | Security monitoring platform |
| Endpoint Monitoring | Sysmon | Windows endpoint telemetry |

---

## Summary

The investigation identified multiple failed RDP login attempts followed by a successful remote login. After gaining access, Microsoft Defender was disabled, a payload was downloaded and placed in the Windows Startup folder for persistence, and a reverse shell connection was established to the attacker's machine. These IOCs can be used to detect similar attacks in future investigations.
