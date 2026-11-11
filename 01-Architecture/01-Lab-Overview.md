**## Project Objective:**

I started this SOC Home Lab as my first practical cybersecurity project to understand my abilities and apply the knowledge I have gained. My objective is to build a hands-on environment where I can explore security tools, monitor system activities, analyze logs, and perform basic security investigations. Through this project, I want to gain practical experience, improve my technical skills, and build confidence in my ability to work in the cybersecurity field. I also see this project as a foundation for learning new technologies and taking on more advanced projects in the future.

**## Lab Workflow**

The SOC Home Lab uses multiple components to collect, forward, and investigate Windows system activities.

1\. Sysmon monitors system activities on the Windows client and generates detailed event records.

2\. These events are stored in the Windows Event Log.

3\. Splunk Universal Forwarder reads the configured Windows Event Logs and forwards the collected data to Splunk Enterprise.

4\. Splunk Enterprise receives and indexes the events.

5\. As a SOC analyst, I use Splunk Search and dashboards to analyze the collected events and investigate suspicious activities.

6\. I document investigation findings and preserve relevant screenshots as evidence.

**### Log Forwarding Details**

\- Protocol: TCP

\- Receiving Port: 9997

\- Forwarder: Splunk Universal Forwarder

\- Destination: Splunk Enterprise on Ubuntu 24.04

