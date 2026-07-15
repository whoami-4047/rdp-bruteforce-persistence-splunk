# MITRE ATT&CK Mapping

This document maps the attack scenario to the MITRE ATT&CK framework.

| Attack Phase | MITRE Tactic | Technique | Technique ID |
|--------------|--------------|-----------|--------------|
| RDP Brute Force | Credential Access | Brute Force | T1110 |
| Successful RDP Login | Lateral Movement | Remote Services: Remote Desktop Protocol | T1021.001 |
| Microsoft Defender Disabled | Defense Evasion | Impair Defenses | T1562.001 |
| Payload Download | Command and Control | Ingress Tool Transfer | T1105 |
| Startup Folder Persistence | Persistence | Boot or Logon Autostart Execution: Startup Items | T1547.001 |
| Payload Execution | Execution | User Execution: Malicious File | T1204.002 |
| Reverse Shell Connection | Command and Control | Application Layer Protocol | T1071 |
