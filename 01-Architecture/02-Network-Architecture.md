# Network Architecture

## Network Configuration

- Virtualization Platform: VMware Workstation 17
- Network Type: Host-only
- Virtual Network: VMnet2
- Network Subnet: 192.168.50.0/24
- DHCP: Disabled

## Virtual Machine Network Details

| Virtual Machine | IP Address | Purpose |
|---|---|---|
| DC01 | 192.168.50.10 | Active Directory and DNS |
| WIN-CLIENT | 192.168.50.20 | Windows client and Sysmon |
| Splunk Ubuntu | 192.168.50.30 | Splunk Enterprise |

## Network Design and Security

I selected a Host-only network for this SOC Home Lab to create an isolated environment for security monitoring and investigation.

Unlike Bridged networking, which connects virtual machines directly to the physical network, Host-only networking keeps communication within the configured virtual network.

This reduces the lab's exposure to external devices and networks while allowing the three virtual machines to communicate with each other.

## Communication Flow

1. WIN-CLIENT communicates with DC01 for DNS resolution and domain services.
2. Sysmon generates event records on WIN-CLIENT.
3. Windows Event Log stores the generated records.
4. Splunk Universal Forwarder collects and forwards the configured logs.
5. Splunk Enterprise receives the forwarded events through TCP port 9997.
6. The SOC analyst searches and investigates the collected events.