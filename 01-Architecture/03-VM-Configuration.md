# Virtual Machine Configuration

## 1. DC01 — Domain Controller

| Configuration | Details |
|---|---|
| Hostname | DC01 | Domain | soclab.test |
| Operating System | Windows Server 2025 |
| IP Address | 192.168.50.10 |
| Domain | soclab.test |
| Main Services | Active Directory Domain Services and DNS |

### Purpose

DC01 acts as the central Domain Controller in the SOC Home Lab.

### Active Directory Domain Services (AD DS)

Active Directory manages domain users, computers, and authentication. It allows domain-connected machines to use centralized identity management.

### Domain Name System (DNS)

DNS resolves domain and computer names into IP addresses. In this lab, WIN-CLIENT uses DC01 as its DNS server to locate domain services and communicate within the domain.





## 2. WIN-CLIENT — Monitoring Endpoint

| Configuration | Details |
|---|---|
| Hostname | WIN-CLIENT |
| Operating System | Windows 11 |
| IP Address | 192.168.50.20 |
| Domain | soclab.test |
| Monitoring Tool | Sysmon |
| Log Forwarding Tool | Splunk Universal Forwarder |

### Purpose

WIN-CLIENT acts as the primary endpoint for generating and monitoring system activities in the SOC Home Lab.

### Sysmon

Sysmon monitors system activities and generates detailed event records, such as process creation events. These records are stored in the Windows Event Log.

### Splunk Universal Forwarder

Splunk Universal Forwarder collects the configured Windows Event Logs and forwards them to Splunk Enterprise for indexing and investigation.






## 3. Splunk Server — Log Management and Investigation

| Configuration | Details |
|---|---|
| Hostname | Splunk Server |
| Operating System | Ubuntu 24.04 |
| IP Address | 192.168.50.30 |
| SIEM Platform | Splunk Enterprise |
| Splunk Version | 10.4.2 |
| Receiving Port | TCP 9997 |
| Index | main |

### Purpose

Ubuntu 24.04 is used to host Splunk Enterprise, which acts as the central log management and investigation platform in this SOC Home Lab.

### Splunk Enterprise

Splunk Enterprise receives event data forwarded by the Splunk Universal Forwarder. It indexes and stores the incoming events, making them searchable.

### Search and Investigation

I use Search Processing Language (SPL) to search, filter, and analyze collected events. This helps me understand system activities, investigate suspicious behavior, and identify relevant security events.