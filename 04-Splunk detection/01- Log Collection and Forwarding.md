# Log Collection and Forwarding

## Environment
- Source: WIN-CLIENT (Windows 11)
- Monitoring: Sysmon
- Log Storage: Windows Event Log
- Forwarder: Splunk Universal Forwarder
- Destination: Ubuntu 24.04 (Splunk Enterprise)
- Receiving Port: TCP 9997
- Index: main

## Verification

I verified that Splunk Universal Forwarder was running on WIN-CLIENT and Splunk Enterprise was running on Ubuntu.

I searched the Sysmon sourcetype in Splunk using:

index=main sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational"

The search returned approximately 20,000 events. I also opened individual events and confirmed that the Sysmon XML event records were readable.

## Result

Sysmon event records are successfully collected, forwarded, indexed, and searchable in Splunk Enterprise.




## Universal Forwarder Configuration

### inputs.conf

Configured to collect:
- Windows Security Event Logs.
- Sysmon Operational Event Logs.

Both inputs are enabled and configured to use the main index.
Sysmon XML rendering is enabled.

### outputs.conf

The Universal Forwarder sends collected events to:

- Destination: 192.168.50.30
- Receiving Port: 9997
- Protocol: TCP

### Verification Result

Both inputs.conf and outputs.conf were checked on WIN-CLIENT.

The forwarding destination matches the Splunk Enterprise server. Log ingestion was independently verified through Splunk Search.