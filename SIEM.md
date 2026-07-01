# SIEM (Security Information and Event Management)

- A SIEM is a platform that collects, aggregates, and analyzes log and event data from across an organization's IT environment (firewalls, servers, endpoints, applications, network devices, etc.) in order to detect, alert on, and help investigate security threats in near real-time.

- SIEM stands for Security Information and Event Management. It's a system that centralizes security monitoring by pulling together two earlier categories of tools:

### SIM (Security Information Management) — long-term log storage, analysis, and reporting

### SEM (Security Event Management) — real-time monitoring, correlation, and alerting

Combined, a SIEM gives an organization one place to collect, analyze, and respond to security data from across its entire network.

  ### How it works, broadly:
- Collection — Agents, syslog forwarders, or API integrations pull log data from many different sources (Windows Event Logs, firewall logs, IDS/IPS alerts, cloud service logs, authentication systems, and so on) into one centralized location.
- Normalization — Since different devices and vendors format logs differently, the SIEM parses and normalizes this data into a consistent structure so it can all be compared and searched together.
- Correlation — The SIEM applies rules (and increasingly, machine learning) to correlate events across multiple sources. For example, a single failed login means nothing, but 50 failed logins from different countries within a minute followed by a successful login is a pattern worth flagging.
- Alerting — When a correlation rule or anomaly threshold is triggered, the SIEM generates an alert for a SOC analyst to investigate, often with a severity/priority score attached.
- Dashboards and reporting — SIEMs provide visualizations, dashboards, and compliance reports so analysts and management can see security posture at a glance.
- Investigation and forensics — Because historical logs are retained and searchable, analysts can pivot back through past events to trace an attacker's actions during incident response (this ties closely into IoCs and the Cyber Kill Chain concepts you've been working with).
Common examples include Splunk, IBM QRadar, Microsoft Sentinel, and the ELK/Elastic Stack.

### How it works — the pipeline

- Log collection — Agents, syslog, or APIs gather logs from firewalls, IDS/IPS, servers, endpoints, applications, and cloud services.
- Normalization — Logs in different formats are translated into a common schema so they can be compared side by side.
- Correlation and rules — The SIEM applies correlation rules (and often ML-based anomaly detection) to spot patterns across multiple log sources that a single log wouldn't reveal on its own.
- Alerting — Suspicious patterns trigger alerts, usually prioritized by severity, sent to the SOC team.
- Dashboards and visualization — Real-time dashboards show overall security posture, active alerts, and trends.
- Investigation/forensics — Historical log data lets analysts trace back through an incident timeline (useful for mapping against frameworks like the Cyber Kill Chain or MITRE ATT&CK).
- Reporting and compliance — Many SIEMs also generate compliance reports (PCI-DSS, HIPAA, etc.).

### If this is for a hands-on project, a typical structure looks like:

- Set up a SIEM tool (Splunk Free, Elastic/ELK Stack, or Wazuh are common free options for student projects)
- Forward logs from a test environment (e.g., a VM, a small home network, or simulated traffic)
- Write or use correlation rules to detect specific attack patterns (brute force login, port scan, malware signature)
- Generate test attacks safely in a lab environment (e.g., using Kali Linux against your own isolated VM) to produce log data.
- Show the alert/dashboard output as your "detection" results
- Document the investigation: what triggered the alert, what log sources confirmed it, and what the recommended response would be.

### Important requirements
Windows 10/11, Linux
RAM: 16 GB, 8
Free SSD space: 80–100 GB
Intel VT-x/AMD-V virtualization enabled in BIOS
Stable internet

- Here i have linux so i am using virtual box for the windows.
- we are going to use windows in virtual box..

  ### Let's get started - Basic overview
  - here i am using Pure Kali linux and i am Gonna install the Virtual machine in Kali linux
  - In Virtual Machine we are running the Windows environment and inside that and using WAZUH for collecting the log's
  - Here we are using Kali linux as Attacker Machine, and in kali linux we are usking 7 Basic Kali linux activities and attacks on our Windows environment after that we will gonaa analyze it. 

- Ping Sweep / Ping Test

- Port Scan

- Service Enumeration

- Failed Login Attempts

- SMB Share Access Attempt

- RDP Connection Attempt

- File Activity Simulation
##  _________________________________________________________________________________

## Let's Get Start the Project:-(All Command for the Kali Linux)

- Use sudo apt update && sudo apt upgrade -y

- sudo apt install virtualbox -y

- after installation Open it with using command "virtualbox".

- <img width="961" height="870" alt="Screenshot_20260630_230559" src="https://github.com/user-attachments/assets/32f3a7b9-9041-40b6-9537-9734e171881b" />

- This Type of Page will open

- we are Going to use the windows 11 in VirtualBox for that we want ISO of that

- we are Downloding the ISO of Windows 11
- Thsis was the official link to download Windows ISO
 https://www.microsoft.com/en-in/software-download/windows11?utm_source=chatgpt.com
- scroll and select this option and after that agan scroll and click on Download Button 
<img width="938" height="888" alt="Screenshot_20260630_233324" src="https://github.com/user-attachments/assets/1d25770e-ce4f-4262-9695-1cfa0330ea13" />

- After that The Windows ISO Will start Downloading, it takes much time like 1-2 Hrs because it was "7.9 GB" ISO File
- https://software.download.prss.microsoft.com/dbazure/Win11_25H2_English_x64_v2.iso?t=246713fd-bed8-43df-881f-db5d642601b5&P1=1782929142&P2=602&P3=2&P4=mI%2bNOFAEQgegPG1rUTyDaQCkyn02ZtZ6nHGtkY%2fGKwfWwHqLLPKpQ4pc1khHC2jE397AWkE%2bw1rpWqdFTQligsGy4Q7TvZ8rVKFCGHjYEZNvNuNYhKtGT%2fT2LNd4VLbNeDVY6ZQuHCTGpVsHx%2b8IJjTiQ2Av%2fTs2IzWc%2fZHmAa6tn1htryFu2ANBm5fjXg81tsiWzTyMywNtI0sqQeK0qUKUbh4jRuIOA4Vqt%2fHfmkINkFggMBFy62NkKfVYyS1Uavtk44Hu%2bfaXzynaWAnQm4JvztJQq5yFz10YS2IaT6wVktJF%2f8lGx%2blNI9%2bdwTTMX92EKCQvXXg6xvl9m7Pbow%3d%3d

- copy This url and directly download the ISO file

- Till then i was giving you guzz a grat tool called Free Download Manager this will encrese the speed and coppy the url what you want to download and pase in it and it will download the file faste as comparitively of Browser.
like here i am downloading the ISO file in just some fue minutes

- <img width="887" height="826" alt="Screenshot_20260701_004706" src="https://github.com/user-attachments/assets/22a99742-cffa-4144-9ab4-170249695db9" />

- return to the project

- Open The VirtualBox and click on New and type Name, Select Folder, TSO image, Type, Version

<img width="1377" height="864" alt="Screenshot_20260701_005521" src="https://github.com/user-attachments/assets/9c1314bf-ccef-4b32-aabb-2c95e22c59bf" />

if comewone want with Unattended installlation, but i am not preffering with Unattended installlation and complete this process fill the information 
<img width="841" height="502" alt="Screenshot_20260701_010343" src="https://github.com/user-attachments/assets/43b58cf6-38f4-4956-8b1c-d706e830ed58" />

- i am going with this method :

- <img width="841" height="502" alt="Screenshot_20260701_010756" src="https://github.com/user-attachments/assets/e9c3b80e-3109-44e9-8bfc-fb818e06d49f" />

- after than click on finish, adter finishing the setup this will come on your screen

  <img width="1377" height="870" alt="Screenshot_20260701_011529" src="https://github.com/user-attachments/assets/7073d743-6bbf-4243-b4dd-8f0d63437f40" />


### SIEM Project — Wazuh + Kali + Windows VM

- PHASE 1 — Lab Setup & Architecture

┌─────────────────────┐         ┌──────────────────────────┐
│   Kali Linux        │         │   Windows 10/11 VM       │
│   (Attacker)        │◄───────►│   (Target / Log Source)  │
│   + Wazuh Server    │         │   + Wazuh Agent          │
│   + Wazuh Dashboard │         │                          │
└─────────────────────┘         └──────────────────────────┘
         │                                   │
         └──────── Same NAT/Host-Only ───────┘
                     Network

### PHASE 2 — Install Wazuh Server on Kali Linux
- Step 1 — System Requirements Check

- Step 2 — Install Wazuh Server in kali linux 
sudo apt update && sudo apt upgrade -y
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
curl -sO https://packages.wazuh.com/4.7/config.yml
chmod +x wazuh-install.sh
sudo bash wazuh-install.sh -a

done Installation here start Wazuh With https>//<Kali Ip>

<img width="1246" height="729" alt="Screenshot_20260701_203847" src="https://github.com/user-attachments/assets/7edc660e-2943-49f1-946b-29a54988a3b4" />

- Now Login with The given username and password and generally username is "admin"
- Wazuh server was done and will download wazuh agent in windows virtual machine 
- go to the Deploy Agent and Fill the information
- enter your base os IP addres in the field of server address
- type agent name as you like.
- then it will generate you an url, command just coppy it and runn this command into Windows PowerShell (Run as Administrator)

  <img width="1025" height="885" alt="Screenshot_20260701_204951" src="https://github.com/user-attachments/assets/55dc4e52-645c-4cf8-86d2-0ed0bae0f4b1" />
