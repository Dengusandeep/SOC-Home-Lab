# RUN-002 — PowerShell Process Investigation

## 1. Incident Overview

| Field | Details |
|---|---|
| Investigation ID | RUN-002 |
| Investigation Type | Process Creation Investigation |
| Host | WIN-CLIENT |
| User | SOCLAB\socuser |
| Operating System | Windows 11 |
| Monitoring Tool | Sysmon |
| SIEM Platform | Splunk Enterprise |
| Event ID | 1 — Process Creation |
| Investigation Status | Completed |
| Activity Classification | Controlled Lab Activity |


## 2. Investigation Objective

The objective of this investigation was to observe PowerShell process creation on the Windows client and understand how parent-child process relationships are established.

The investigation focused on examining Sysmon Event ID 1 and using ProcessGuid and ParentProcessGuid to trace process execution relationships.

Splunk Enterprise was used to search and analyze the collected events.

## 3. Environment and Tools
| Component | Details |
|---|---|
| Endpoint | WIN-CLIENT |
| Operating System | Windows 11 |
| Domain | soclab.test |
| Monitoring | Sysmon |
| Log Collection | Splunk Universal Forwarder |
| SIEM | Splunk Enterprise 10.4.2 |
| Log Index | main |


## 4. Activity Observed
A controlled PowerShell activity was executed on WIN-CLIENT to generate process creation events.

### Command Executed

powershell.exe -NoProfile -Command "Start-Sleep -Seconds 15"

### Observed Process

| Field | Value |
|---|---|
| Event ID | 1 |
| Process Name | powershell.exe |
| Process ID | 6764 |
| User | SOCLAB\socuser |
| Command | Start-Sleep -Seconds 15 |
| Parent Process | powershell.exe |

The activity was performed intentionally as part of the SOC Home Lab investigation.


## 5. Investigation and Analysis
I searched for the PowerShell process creation event in Splunk using its Process ID.

I examined the following Sysmon fields:

- ProcessGuid
- ParentProcessGuid
- ProcessId
- ParentProcessId
- Image
- ParentImage
- CommandLine
- User

I used ParentProcessGuid from the child process to identify its parent by matching it with the ProcessGuid of another event.

This helped establish the parent-child process relationships and understand how PowerShell was launched through Windows Terminal.


## 6. Findings
1. Sysmon successfully recorded the PowerShell process creation event (Event ID 1).
2. Splunk Enterprise successfully received and indexed the event.
3. The investigated PowerShell process had PID 6764.
4. Parent-child relationships were examined using ProcessGuid and ParentProcessGuid.
5. The observed command was a controlled Start-Sleep activity.
6. The examined activity was consistent with the intended lab experiment.

## 7. Conclusion
The investigation successfully demonstrated how Sysmon records process creation events and how Splunk can be used to investigate process execution relationships.

This exercise improved my understanding of process monitoring, parent-child relationships, and event analysis using SPL.

No evidence of malicious behavior was identified in the events examined.

## 8. Evidence
The following screenshots support the investigation findings.

| Evidence | Screenshot | Description |
|---|---|---|
| 1 | 01-RUN-002-Process-Creation.png | Sysmon PowerShell process creation event (PID 6764). |
| 2 | 02-RUN-002-Parent-PowerShell.png | Parent PowerShell process event (PID 6584). |
| 3 | 03-RUN-002-WindowsTerminal.png | Windows Terminal process event. |

All screenshots are stored in the project's 05-Evidence-screenshot folder.