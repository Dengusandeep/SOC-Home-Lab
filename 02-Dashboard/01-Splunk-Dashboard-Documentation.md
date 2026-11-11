# Splunk Security Monitoring Dashboard

## 1. Dashboard Overview

I created a dashboard in Splunk Enterprise to visualize Sysmon event activity collected from the Windows 11 client (WIN-CLIENT).

The dashboard provides a graphical view of event activity over time, making it easier to understand event patterns and monitor the collected logs.

## 2. Dashboard Objective

The objective of this dashboard is to provide a visual overview of Sysmon events collected from WIN-CLIENT.

It helps me monitor event volume over time, understand activity patterns, and identify periods of increased event activity that may require further investigation.

## 3. Dashboard Panels

### Sysmon Events Over Time

| Configuration | Details |
|---|---|
| Panel Name | Sysmon Events Over Time |
| Visualization | Line Chart |
| Data Source | Sysmon Operational Logs |
| Index | main |
| X-Axis | Event timestamp (_time) |
| Y-Axis | Event count |
| Time Interval | 15 minutes |

### Panel Description

This panel displays the number of Sysmon events recorded during different time intervals.

The graph uses spikes to represent periods with increased event activity.

## 4. SPL Queries

### Sysmon Events Over Time

Query:

index=main sourcetype="xmlwineventlog:microsoft-windows-sysmon/operational"
| timechart span=15m count

### Query Explanation

- `index=main` – Searches events stored in the main index.
- `sourcetype` – Filters for Sysmon Operational logs.
- `timechart` – Displays event counts over time.
- `span=15m` – Groups events into 15-minute intervals.
- `count` – Counts the number of events in each interval.

### Purpose

This query helps visualize Sysmon event volume over time and identify periods of increased activity.

## 5. Dashboard Analysis

The Sysmon Events Over Time panel displays the number of collected Sysmon events across different time intervals.

The spikes represent periods when more events were recorded, while the flat portions represent periods with fewer events.

This visualization helps me understand event activity over time and identify periods that may require further investigation.

An increase in event volume does not automatically indicate malicious activity. Further investigation is required to understand the reason behind unusual activity.

## 6. Conclusion

The Splunk dashboard provides a visual overview of Sysmon event activity collected from WIN-CLIENT.

Through this dashboard, I learned how to use SPL timechart commands to visualize event data and monitor activity patterns.

This dashboard provides a starting point for security monitoring and can be expanded with additional panels and detection queries in future improvements.