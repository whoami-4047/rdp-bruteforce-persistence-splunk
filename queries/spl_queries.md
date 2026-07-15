# Splunk SPL Queries

This document contains the SPL queries used during the SOC investigation.

---

## Step 1 - Failed RDP Logins

```spl
host="<HOSTNAME>" EventCode=4625
| table _time Account_Name Source_Network_Address Failure_Reason
```

---

## Step 2 - Successful RDP Login

```spl
host="<HOSTNAME>" EventCode=4624 source="WinEventLog:Security" Logon_Type=10   | table _time Account_Name  Source_Network_Address
```

---

## Step 3 - Microsoft Defender Disabled

```spl
host="<HOSTNAME>"
| search Defender OR "Windows Defender"
| table _time EventCode Message
```

---

## Step 4 - Payload Download

```spl
host="<HOSTNAME>" sourcetype=XmlWinEventLog EventCode=11 | table _time TargetFilename Image User
```

---

## Step 5 - Startup Folder Persistence

```spl
host="<HOSTNAME>" sourcetype=XmlWinEventLog EventCode=11 TargetFilename=*startup* | table _time TargetFilename Image User
```

---

## Step 6 - Payload Execution

```spl
host="<HOSTNAME>" sourcetype=XmlWinEventLog EventCode=1  | table _time Image CommandLine ParentImage User
```

---

## Step 7 - Reverse Shell Connection

```spl
host="<HOSTNAME>" sourcetype=XmlWinEventLog EventCode=3  | table _time Image DestinationIp DestinationPort Protocol SourceIp
```

---

## Step 8 - Attack Timeline

```spl
host="<HOSTNAME>"  ( EventCode=4624 OR EventCode=4625 OR EventCode=1 OR EventCode=3 OR EventCode= 11) | timechart span=1m count by EventCode
```

---

## Step 9 - Statistics

```spl
host="<HOSTNAME>"  ( EventCode=4624 OR EventCode=4625 OR EventCode=1 OR EventCode=3 OR EventCode= 11) | stats count by EventCode
| eval Event=case(
    EventCode=4625,"Failed RDP Logins",
    EventCode=4624,"Successful RDP Login",
    EventCode=1,"Process Execution",
    EventCode=3,"Network Connection",
    EventCode=11,"File Creation"
)
| table Event count
```

---

## Step 10 - Detection Rule

```spl
host="<HOSTNAME>" EventCode=4624 sourcetype="WinEventLog:Security" LogonType=10
| table _time Account_Name Source_Network_Address ComputerName
```
