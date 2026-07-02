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
- Get the Iso from official site

- copy This url and directly download the ISO file

- Till then i was giving you a great tool called Free Download Manager this will encrese the speed and coppy the url what you want to download and pase in it and it will download the file faste as comparitively of Browser.
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

<img width="1536" height="1024" alt="08c4c048-27f2-4cdc-8e0c-12a07bb352c2" src="https://github.com/user-attachments/assets/f672e0ac-0a5e-47a4-bc48-3723c061813d" />


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

<img width="916" height="766" alt="Screenshot_20260701_094246" src="https://github.com/user-attachments/assets/e1e8ae87-23b0-45bd-baab-8e5184132e9d" />

 ### Installing Wazuh Agent on Windows 11
**Step 1: Download the Wazuh Agent**
- Open any web browser on the Windows virtual machine.
- Visit the official Wazuh website.
- Navigate to Downloads → Wazuh Agent → Windows.
- Download the latest Windows Agent installer (.msi).

  **Step 2: Run the Installer**
- Locate the downloaded .msi installer.
- Double-click the installer.
- If the User Account Control (UAC) prompt appears, click Yes.
- The Wazuh Agent Setup Wizard opens.

  **Step 3: Accept the License Agreement**
- Read the License Agreement.
- Select I accept the agreement.
- Click Next.
- <img width="912" height="1005" alt="Screenshot_20260701_091524" src="https://github.com/user-attachments/assets/132e6518-2de2-4184-b4d7-546b1fd57203" />


**Step 4: Specify the Installation Directory**
- The default installation path is:
C:\Program Files (x86)\ossec-agent\  then click next

**Step 5: Configure the Wazuh Manager**
- During installation, the setup wizard asks for the Manager Address.
- Enter the IP address of the Kali Linux machine running the Wazuh Manager.
Example:Manager Address:192.168.56.101

**Step 6: Install the Agent**
Click Install.
The installer copies all required files and installs the Wazuh Agent service.
Wait until the installation completes.
Click Finish.

**Step 7: Verify the Installation**
- Open Command Prompt as Administrator and run:
- sc query WazuhSvc
- Expected output:STATE : 4 RUNNING

 **Step 8: Verify the Configuration File**
- Open the configuration file located at:
- C:\Program Files (x86)\ossec-agent\ossec.conf
- Verify that the manager IP address is correctly configured.
<client>
    <server>
        <address>192.168.56.101</address>
        <port>1514</port>
        <protocol>tcp</protocol>
    </server>
</client>
 **Connecting Agent to Wazuh Manager**
curl -o wazuh-agent.deb https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.9.0-1_amd64.deb
sudo WAZUH_MANAGER='<WAZUH-MANAGER-IP>' dpkg -i ./wazuh-agent.deb
sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent

**Step 9: Verify Agent Registration**
On the Kali Linux Wazuh Manager, execute:
<img width="927" height="844" alt="Screenshot_20260701_092747" src="https://github.com/user-attachments/assets/01df8e8d-3750-4306-9f24-273c1dc0b2e2" />
sudo /var/ossec/bin/agent_control -l
Expected output:

Wazuh agent_control. List of available agents:
   ID: 000, Name: wazuh-manager (server), IP: 127.0.0.1, Active
   ID: 001, Name: victim-linux, IP: 192.168.56.11, Active
   ID: 002, Name: victim-win, IP: 192.168.56.12, Active

### Attack on Windows virtual machine 
**Ping Sweep**
- nmap -sn 192.168.46.<img width="423" height="49" alt="Screenshot_20260702_153811" src="https://github.com/user-attachments/assets/4fbb8a1a-8eb3-41ea-85d0-084f0686c0d2" />
0/24
<img width="907" height="1004" alt="Screenshot_20260702_153459" src="https://github.com/user-attachments/assets/15afcb06-228f-4ca7-a807-f295533ff01d" />

<img width="423" height="49" alt="Screenshot_20260702_153811" src="https://github.com/user-attachments/assets/0af55157-2a8a-4c5f-b1fc-1f10e22c0016" />

**- Port Scan**
nmap -sS -T4 -p- 192.168.56.11
<img width="918" height="647" alt="Screenshot_20260702_160914" src="https://github.com/user-attachments/assets/ce6908b9-97ac-4d77-9a26-e987624464d7" />

**- Service Enumeration**
- nmap -sV -sC -p 21,22,80,139,445,3389 192.168.56.11 -oN service_enum.txt
-sV = version detection
-sC = default NSE scripts

<img width="721" height="925" alt="Screenshot_20260702_161644" src="https://github.com/user-attachments/assets/4168df1f-cd3d-4852-82e1-5c3c2f585f9c" />

**Brute Force Login**
hydra -l admin -P /usr/share/wordlists/rockyou.txt ssh://192.168.56.11 -t 4 -f

**SMB Enumeration**
enum4linux -a 192.168.56.12
smbclient -L //192.168.56.12/ -N
nmap --script smb-enum-shares,smb-enum-users -p 445 192.168.56.12

<img width="616" height="966" alt="Screenshot_20260702_174518" src="https://github.com/user-attachments/assets/d51ecb3a-e41e-4648-92ac-05b250dabcb6" />


**- Now this Attacks was Done and now we gonna moving toward the windows vb and log analysing**
start the wazuh and see all the logs and extract differt want from it on the basis of usuage
<img width="1913" height="961" alt="Screenshot_20260702_183605" src="https://github.com/user-attachments/assets/8b6c9f4e-c3d2-4414-842b-7a463d01e883" />

Successful logon                         4624
Failed logon                             4625
Logon using explicit credentials         4648
New service installed                    7045
RDP user authentication succeeded        1149  

- enter that event id manualy in that dashboard and you will get the log of that then we will generate allert of that id
  
<img width="1592" height="737" alt="Screenshot_20260703_002601" src="https://github.com/user-attachments/assets/379f9c07-18b8-4481-b579-bfef07573327" />

**Alert Generation**
The alert threshold is configured in the /var/ossec/etc/ossec.conf configuration file on the Wazuh server within the <alerts> XML tag.

The code block below shows the default alert threshold configuration for events and forwarding alerts via email:


<ossec_config>
  <alerts>
    <log_alert_level>3</log_alert_level>
    <email_alert_level>12</email_alert_level>
  </alerts>
</ossec_config>

- The <log_alert_level> tag sets the minimum severity level to trigger alerts stored in the /var/ossec/logs/alerts/alerts.log and/or the /var/ossec/logs/alerts/alerts.json file. The default value is 3. The allowed value is any integer from 1 to 16 as referenced in the rules classification guide.

- The <email_alert_level> tag sets the minimum severity level for an alert to generate an email notification. The default value is 12. The allowed value is any integer from 1 to 16. This setting overrides granular email alert configuration. However, the alert_by_email option within individual rules can override both global and granular alert level thresholds to trigger an email alert.

## Conclusion
- This project successfully demonstrated the collection, monitoring, and analysis of Windows Security Events using the Wazuh SIEM platform. Windows Event Logs were collected through the Wazuh Agent, parsed and normalized by the Wazuh Manager, and analyzed using predefined and custom detection rules. Important security events such as successful logins (4624), failed logins (4625), explicit credential usage (4648), new service installation (7045), and successful RDP authentication (1149) were monitored in real time.

- The project showed how SIEM solutions can automate log collection, event correlation, threat detection, and alert generation, enabling security analysts to identify suspicious activities such as brute-force attacks, credential misuse, unauthorized service creation, and remote access attempts. The Wazuh Dashboard provided centralized visibility for investigating alerts and responding to potential security incidents.

- Overall, the implementation demonstrates that Wazuh is an effective open-source SIEM platform for improving system monitoring, enhancing threat detection capabilities, and supporting incident response in Windows environments.
