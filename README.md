# SOC-Home-Lab
Hands-on SOC Analyst L1 home lab — attack simulation, Splunk log investigation, MITRE ATT&amp;CK mapping, and incident escalation practice
<img width="600" height="800" alt="1" src="https://github.com/user-attachments/assets/83f856d5-4521-4608-b97e-ce61d35c2571" />
<h2>📋 Project Summary</h2>

<p>
This repository documents my self-built <strong>Security Operations Center (SOC) Home Lab</strong>,
designed to simulate real-world cyber attacks and perform end-to-end security investigations using
<strong>Splunk Enterprise</strong> as the centralized SIEM platform.
</p>

<p>
The lab consists of <strong>Kali Linux (Attacker)</strong>,
<strong>Ubuntu Server (Target Server)</strong>,
<strong>Ubuntu GUI (Splunk Enterprise)</strong>, and
<strong>Windows 10 (Victim Endpoint)</strong>.
It includes <strong>Suricata IDS</strong>,
<strong>Apache2 with ModSecurity (WAF)</strong>,
<strong>Docker (DVWA &amp; OWASP Juice Shop)</strong>,
<strong>Sysmon</strong>, and
<strong>Splunk Universal Forwarders</strong> to generate, collect, and analyze security events from multiple sources.
</p>

<p>
The primary objective of this project is to gain hands-on experience with
<strong>SOC Analyst L1</strong> responsibilities, including threat detection,
log analysis, incident investigation, MITRE ATT&amp;CK mapping, and security event validation
within a realistic enterprise-style environment.
</p>

<hr>

<h3>🎯 Attack Scenarios Covered</h3>

<ul>
    <li>🔍 Reconnaissance &amp; Active Scanning (Nmap)</li>
    <li>🔐 SSH Brute Force (Hydra)</li>
    <li>🌐 SQL Injection</li>
    <li>⚡ Cross-Site Scripting (XSS)</li>
    <li>📂 Directory Brute Force (Gobuster)</li>
    <li>💻 Command Injection</li>
    <li>📤 File Upload Exploitation</li>
    <li>📁 FTP Data Exfiltration</li>
    <li>🪟 Windows PowerShell Abuse</li>
    <li>🔑 Credential Dumping</li>
    <li>📧 Phishing Email Analysis</li>
    <li>🔗 Multi-Stage Attack Chain Investigation</li>
</ul>

<hr>

<h3>🔎 Each Investigation Includes</h3>

<ul>
    <li>Attack Simulation</li>
    <li>Log Collection &amp; Analysis</li>
    <li>Splunk Detection Queries (SPL)</li>
    <li>IOC Identification</li>
    <li>Evidence Collection</li>
    <li>True Positive / False Positive Validation</li>
    <li>MITRE ATT&amp;CK Mapping</li>
    <li>Incident Timeline</li>
    <li>Impact Assessment</li>
    <li>SOC Analyst L1 Investigation Report</li>
    <li>L1 → L2 Escalation Decision (where applicable)</li>
</ul>
<h2>🏗️ SOC Analyst L1 Home Lab Architecture</h2>
<p>
This home lab simulates a <strong>real-world Security Operations Center (SOC)</strong>
environment for practicing <strong>threat detection</strong>,
<strong>log analysis</strong>, <strong>incident investigation</strong>, and
<strong>incident response</strong>.
</p>
<p>
The lab is built using <strong>VMware Workstation</strong>, with all virtual
machines connected through a <strong>NAT network</strong> for secure communication.
</p>
<img width="600" height="800" alt="2" align="center" src="https://github.com/user-attachments/assets/2f0e0536-eaad-40ca-b6f9-fe8bcc220e22" />
<h2>🖥️ Lab Components</h2>
<ul>
  <li>
    <strong>🐉 Kali Linux</strong><br>
    Attacker machine used to perform penetration testing, reconnaissance,
    brute-force attacks, web application testing, and network scanning.
  </li>
  <br>
  <li>
    <strong>🐧 Ubuntu Server</strong><br>
    Target server hosting vulnerable applications
    (<strong>DVWA</strong> &amp; <strong>OWASP Juice Shop</strong>),
    Suricata IDS, Syslog, and log sources for security monitoring.
  </li>
  <br>
  <li>
    <strong>📊 Ubuntu Desktop (Splunk Enterprise)</strong><br>
    Centralized SIEM platform responsible for collecting, indexing,
    searching, and analyzing logs from all systems.
  </li>

  <br>
  <li>
    <strong>🪟 Windows 10</strong><br>
    Victim endpoint used to generate Windows Event Logs, RDP, SMB,
    authentication, and user activity for SOC investigations.
  </li>
</ul>

<h2>📊 Splunk Enterprise Setup (Ubuntu GUI)</h2>

<p>
This section covers the installation and initial configuration of
<strong>Splunk Enterprise</strong> on the <strong>Ubuntu GUI</strong> virtual machine,
which serves as the central <strong>SIEM (Security Information and Event Management)</strong>
server for this home lab.
</p>
<img width="600" height="800" alt="5" src="https://github.com/user-attachments/assets/eb42960f-cf35-46b4-8ac8-04484c488794" />
<p>
After the installation is complete, the Ubuntu GUI machine will collect,
index, and analyze logs received from the Ubuntu Server and Windows 10
systems through the <strong>Splunk Universal Forwarder</strong>.
</p>

<hr>
<h3>💡 Lab Environment</h3>

<ul>
  <li><strong>Operating System:</strong> Ubuntu Desktop 22.04 LTS</li>
  <li><strong>Role:</strong> Splunk Enterprise (SIEM Server)</li>
</ul>

<p>
Once configured, this server becomes the centralized platform for
security monitoring, threat detection, log analysis, and incident
investigation throughout the SOC Home Lab.
</p>
<h2>🛡️ Ubuntu Server - Suricata IDS & Apache2 + ModSecurity (WAF)</h2>

<p>
This section covers the installation and configuration of
<strong>Suricata IDS</strong> and
<strong>Apache2 with ModSecurity (WAF)</strong>
on the <strong>Ubuntu Server</strong>.
These security tools provide both
<strong>network intrusion detection</strong> and
<strong>web application protection</strong> within the SOC Home Lab.
</p>

<p>
Suricata continuously monitors network traffic for suspicious activity,
while Apache2 with ModSecurity protects vulnerable web applications by
detecting and blocking malicious HTTP requests using the OWASP Core Rule Set (CRS).
</p>
<img width="600" height="800" alt="3" src="https://github.com/user-attachments/assets/0f8dc138-dcbe-4a9b-916c-8e460526b517" />

<hr>

<h3>🎯 Objectives</h3>

<ul>
<li>Install and configure Suricata IDS.</li>
<li>Update and enable the latest detection rules.</li>
<li>Configure the HOME_NET variable for the lab network.</li>
<li>Install Apache2 and ModSecurity WAF.</li>
<li>Deploy the OWASP Core Rule Set (CRS).</li>
<li>Enable Reverse Proxy for DVWA and Juice Shop.</li>
<li>Detect and block common web attacks.</li>
<li>Generate security logs for Splunk analysis.</li>
</ul>

<hr>

<h3>💡 Lab Environment</h3>

<ul>
<li><strong>Operating System:</strong> Ubuntu Server 22.04 LTS</li>
<li><strong>Role:</strong> Target Server</li>
<li><strong>Installed Services:</strong> Suricata IDS, Apache2, ModSecurity WAF</li>
<li><strong>Purpose:</strong> Network Monitoring & Web Application Protection</li>
</ul>

<h2>🐧 Ubuntu Server - Docker, DVWA, Juice Shop & Splunk Universal Forwarder</h2>

<p>
This section explains how the <strong>Ubuntu Server</strong> is configured as
the primary target server within the SOC Home Lab.
It hosts vulnerable web applications inside Docker containers while
forwarding security logs to the centralized
<strong>Splunk Enterprise SIEM</strong>.
</p>

<p>
Docker is used to deploy
<strong>DVWA (Damn Vulnerable Web Application)</strong> and
<strong>OWASP Juice Shop</strong>,
allowing realistic attack simulations for SOC investigations.
The <strong>Splunk Universal Forwarder</strong> collects system,
network, web application, and IDS logs before securely forwarding
them to the Splunk Server for monitoring and analysis.
</p>
<img width="600" height="800" alt="4" src="https://github.com/user-attachments/assets/ad628e10-9a5d-4fb5-be9f-005ad2e23f28" />

<hr>

<h3>🎯 Objectives</h3>

<ul>
<li>Install and configure Docker.</li>
<li>Deploy DVWA and OWASP Juice Shop containers.</li>
<li>Verify Docker services and container status.</li>
<li>Access applications through Apache Reverse Proxy.</li>
<li>Install Splunk Universal Forwarder.</li>
<li>Configure log forwarding to Splunk Enterprise.</li>
<li>Monitor Linux, Apache, Suricata and Docker logs.</li>
<li>Generate attack data for SOC detection and investigation.</li>
</ul>

<hr>

<h3>💡 Lab Environment</h3>

<ul>
<li><strong>Operating System:</strong> Ubuntu Server 22.04 LTS</li>
<li><strong>Role:</strong> Target Server</li>
<li><strong>Applications:</strong> DVWA & OWASP Juice Shop (Docker)</li>
<li><strong>Log Forwarder:</strong> Splunk Universal Forwarder</li>
<li><strong>Purpose:</strong> Attack Simulation & Log Collection</li>
</ul>

<h2>🪟 Windows 10 - Sysmon & Splunk Universal Forwarder</h2>

<p>
This section covers the installation and configuration of
<strong>Sysmon</strong> and the
<strong>Splunk Universal Forwarder</strong>
on the <strong>Windows 10</strong> endpoint.
The endpoint generates detailed Windows telemetry and securely forwards
security logs to the <strong>Splunk Enterprise SIEM</strong> running on the Ubuntu GUI server.
</p>

<p>
Sysmon enhances native Windows logging by recording detailed process,
network, file creation, registry, and system events.
The Splunk Universal Forwarder continuously collects these logs and
sends them to Splunk Enterprise for centralized monitoring,
threat detection, and incident investigation.
</p>

<hr>
<img width="600" height="800" alt="6" src="https://github.com/user-attachments/assets/2d85f49e-e65e-4315-8af5-bf65781e8693" />

<h3>🎯 Objectives</h3>

<ul>
<li>Install Microsoft Sysmon using the SwiftOnSecurity configuration.</li>
<li>Verify the Sysmon service and operational event logs.</li>
<li>Install Splunk Universal Forwarder on Windows 10.</li>
<li>Configure inputs.conf to collect Windows Event Logs.</li>
<li>Forward Security, System and Sysmon logs to Splunk Enterprise.</li>
<li>Create and verify the <strong>soc_endpoint</strong> index in Splunk.</li>
<li>Validate successful log ingestion and endpoint visibility.</li>
<li>Generate endpoint telemetry for SOC investigations.</li>
</ul>

<hr>

<h3>💡 Lab Environment</h3>

<ul>
<li><strong>Operating System:</strong> Windows 10 Pro</li>
<li><strong>Role:</strong> Victim Endpoint</li>
<li><strong>Installed Components:</strong> Sysmon & Splunk Universal Forwarder</li>
<li><strong>Log Sources:</strong> Security, System & Sysmon Event Logs</li>
<li><strong>Purpose:</strong> Endpoint Monitoring & Log Forwarding</li>
</ul>

<h2>Workflow</h2>
<img width="800" height="1200" alt="image" src="https://github.com/user-attachments/assets/77715668-f3ec-4bee-ab83-f6270d2e26b6" />
