##SPL
index=main sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" "6764"

Purpose:
Searches the Sysmon event records for the process ID 6764.

Investigation findings:
- Event ID: 1 — Process Creation
- Process: powershell.exe
- Process ID: 6764
- Command: Start-Sleep -Seconds 15


## 1. Investigation Objective

I generated a controlled PowerShell process on WIN-CLIENT to observe how process creation is recorded by Sysmon.

The objective was to understand how a process starts, how parent and child processes are created, and how their relationships can be traced using ProcessGuid and ParentProcessGuid.

Through this investigation, I wanted to understand the process execution flow from the initial application to its child processes and how a SOC analyst can investigate these relationships using Splunk.


## 2. Controlled Activity
| Field | Value |
|---|---|
| Machine | WIN-CLIENT |
| Activity | PowerShell process creation |
| Command | `powershell.exe -NoProfile -Command "Start-Sleep -Seconds 15"` |
| Sysmon Event ID | 1 |
| Purpose | Observe process creation and parent-child relationships |


## 3. SPL Investigation
index=main sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" "6764"

Purpose: Search for the Sysmon event containing process ID 6764.

Finding:
- Process: powershell.exe
- Process ID: 6764
- Event ID: 1
- Command: Start-Sleep -Seconds 15


## 4. Parent-Child Process Investigation

During the investigation, I examined the ProcessGuid and ParentProcessGuid fields in Sysmon Event ID 1.

I used the ParentProcessGuid of the child process to identify its parent process. I then compared it with the ProcessGuid of other events to establish the process relationship.

### Identified Processes

| Process | PID | Parent |
|---|---:|---|
| WindowsTerminal.exe | 9712* | explorer.exe |
| powershell.exe | 6584 | WindowsTerminal.exe |
| powershell.exe | 6764 | powershell.exe |

*PID requires verification against the original event because the recorded ParentProcessId was 9772.

### Investigation Method

- ProcessGuid identifies a specific process instance.
- ParentProcessGuid identifies the process that created it.
- Matching the child's ParentProcessGuid with the parent's ProcessGuid helps establish the relationship.


## 5. Investigation Conclusion

The investigated PowerShell activity was generated intentionally as part of a controlled SOC Home Lab exercise.

Sysmon recorded the process creation events, and Splunk allowed me to examine the process details and parent-child relationships.

Based on the observed command, process information, and execution context, the activity was consistent with the intended lab activity. No evidence of malicious behavior was identified in the events examined.

This investigation helped me understand process creation, parent-child relationships, and how ProcessGuid and ParentProcessGuid can be used during SOC investigations.