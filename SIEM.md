# SIEM (Security Information and Event Management)

- A SIEM is a platform that collects, aggregates, and analyzes log and event data from across an organization's IT environment (firewalls, servers, endpoints, applications, network devices, etc.) in order to detect, alert on, and help investigate security threats in near real-time.

  ### How it works, broadly:
- Collection — Agents, syslog forwarders, or API integrations pull log data from many different sources (Windows Event Logs, firewall logs, IDS/IPS alerts, cloud service logs, authentication systems, and so on) into one centralized location.
- Normalization — Since different devices and vendors format logs differently, the SIEM parses and normalizes this data into a consistent structure so it can all be compared and searched together.
- Correlation — The SIEM applies rules (and increasingly, machine learning) to correlate events across multiple sources. For example, a single failed login means nothing, but 50 failed logins from different countries within a minute followed by a successful login is a pattern worth flagging.
- Alerting — When a correlation rule or anomaly threshold is triggered, the SIEM generates an alert for a SOC analyst to investigate, often with a severity/priority score attached.
- Dashboards and reporting — SIEMs provide visualizations, dashboards, and compliance reports so analysts and management can see security posture at a glance.
- Investigation and forensics — Because historical logs are retained and searchable, analysts can pivot back through past events to trace an attacker's actions during incident response (this ties closely into IoCs and the Cyber Kill Chain concepts you've been working with).
Common examples include Splunk, IBM QRadar, Microsoft Sentinel, and the ELK/Elastic Stack.

### Importand requirements
Windows 10/11, Linux
RAM: 16 GB, 8
Free SSD space: 80–100 GB
Intel VT-x/AMD-V virtualization enabled in BIOS
Stable internet

- Here i have linux so i am using virtual box for the windows
- we are going to use windows in virtual box


