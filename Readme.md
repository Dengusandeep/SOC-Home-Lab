# SOC Home Lab — Network Monitoring & Security Investigation

## 1. Project Overview

This project is a hands-on Security Operations Center (SOC) home lab built to practice endpoint monitoring, centralized log collection, security event analysis, and investigation using Splunk.

The lab simulates a small Windows domain environment where endpoint activities are monitored using Sysmon and forwarded to Splunk for analysis.

## 2. Lab Architecture

The lab runs on VMware Workstation 17 using a Host-only network.

| Machine | Operating System | IP Address | Purpose |
|---|---|---|---|
| DC01 | Windows Server 2025 | 192.168.50.10 | Active Directory and DNS |
| WIN-CLIENT | Windows 11 | 192.168.50.20 | Endpoint monitoring |
| Splunk Server | Ubuntu 24.04 | 192.168.50.30 | Centralized log collection and analysis |

- Domain: `soclab.test`
- Network: `192.168.50.0/24`
- Splunk Receiving Port: `9997`
- Splunk Index: `main`

## 3. Tools and Technologies

- VMware Workstation 17
- Windows Server 2025
- Windows 11
- Ubuntu 24.04
- Active Directory Domain Services
- DNS
- Sysmon
- Splunk Universal Forwarder
- Splunk Enterprise 10.4.2
- Search Processing Language (SPL)

## 4. Log Collection Workflow

1. User activity occurs on the Windows endpoint.
2. Sysmon monitors system activity and generates event records.
3. Windows Event Log stores the generated records.
4. Splunk Universal Forwarder collects the logs.
5. The forwarder sends logs to Splunk Enterprise over TCP port 9997.
6. Splunk indexes the events for searching and investigation.
7. SPL queries are used to analyze the collected data.

## 5. Log Collection Verification

Sysmon Operational logs were successfully received in Splunk.

Index: `main`

Sourcetype: `XmlWinEventLog:Microsoft-Windows-Sysmon/Operational`

Verification query:

`index=main sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational"`

Approximately 20,000 events were visible during verification.

## 6. Security Investigation — RUN-002

Investigation: PowerShell Process Creation

Objective: Understand process creation events and parent-child process relationships using Sysmon Event ID 1.

A controlled PowerShell command was executed:

`powershell.exe -NoProfile -Command "Start-Sleep -Seconds 15"`

The investigation examined:

- Process ID
- Parent Process ID
- Process GUID
- Parent Process GUID
- Image
- Parent Image
- Command Line
- User

The investigation demonstrated how Sysmon process creation events can help an analyst understand process relationships.

Finding: The observed activity was consistent with the controlled lab experiment. No evidence of malicious behavior was identified in the events examined.

Detailed report: `Incident-Report/RUN-002-PowerShell-Process-Investigation.md`

## 7. Splunk Dashboard

A Splunk dashboard named SOC Home Lab Dashboard was created.

It contains a panel named Sysmon Events Over Time, which visualizes the number of Sysmon events received over 15-minute intervals.

The dashboard provides a high-level view of endpoint event activity.

## 8. Project Documentation

- `Architecture/` — Lab overview, network architecture, and VM configuration.
- `Splunk detection/` — Log collection, forwarding, and process investigation.
- `Incident-Report/` — RUN-002 investigation report.
- `Dashboard/` — Splunk dashboard documentation.
- `05-Evidence-screenshot/` — Screenshots supporting the lab work.
- `Network Troubleshooting.txt` — Network troubleshooting notes.

## 9. Key Learnings

- Building an isolated virtual lab environment.
- Configuring Windows domain services.
- Understanding Sysmon event generation.
- Forwarding Windows logs to Splunk.
- Verifying centralized log ingestion.
- Searching and analyzing events using SPL.
- Investigating process creation and parent-child relationships.
- Visualizing event activity using a Splunk dashboard.

## 10. Project Status

This is an ongoing practical learning project. Additional detection use cases, investigations, and dashboard panels may be added as the lab develops.