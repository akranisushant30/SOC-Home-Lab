<h1>Chapter 17 — Networking for SOC L1</h1>
<img width="800" height="1200" alt="image" src="https://github.com/user-attachments/assets/78dbfe0c-abce-48b2-8ddb-ddc229bc8054" />

<p>
This chapter focuses on how a <strong>SOC L1 analyst</strong> understands
and investigates network activity using IP addresses, ports, protocols,
traffic direction, and network logs.
</p>

<hr>

<h2>17.1 Source &amp; Destination IP in SOC Analysis</h2>

<p>
Every network connection has a <strong>source</strong> and a
<strong>destination</strong>.
</p>

<ul>
  <li><strong>Source IP</strong> → The system where the traffic came from</li>
  <li><strong>Destination IP</strong> → The system where the traffic is going</li>
</ul>

<p><strong>Example:</strong></p>

<pre>
Source IP:       192.168.1.25
Destination IP:  8.8.8.8
</pre>

<p>
A SOC analyst may check:
</p>

<ul>
  <li>Is the source internal or external?</li>
  <li>Is the destination internal or external?</li>
  <li>Are these systems expected to communicate?</li>
  <li>Is one source contacting many destinations?</li>
  <li>Is the IP known or unusual?</li>
</ul>

<p>
<strong>Simple meaning:</strong><br>
Source IP = Where traffic came from<br>
Destination IP = Where traffic went
</p>

<hr>

<h2>17.2 Ports &amp; Protocols in SOC Analysis</h2>

<p>
<strong>Ports</strong> help identify which network service may be involved,
while <strong>protocols</strong> show how the systems are communicating.
</p>

<p><strong>Example:</strong></p>

<pre>
Destination IP:    10.0.0.20
Destination Port:  22
Protocol:          TCP
</pre>

<p>
Port <code>22</code> is commonly associated with SSH.
</p>

<table>
  <thead>
    <tr>
      <th>Port</th>
      <th>Common Service</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>22</td>
      <td>SSH</td>
    </tr>
    <tr>
      <td>53</td>
      <td>DNS</td>
    </tr>
    <tr>
      <td>80</td>
      <td>HTTP</td>
    </tr>
    <tr>
      <td>443</td>
      <td>HTTPS</td>
    </tr>
    <tr>
      <td>3389</td>
      <td>RDP</td>
    </tr>
  </tbody>
</table>

<p>
A SOC analyst uses the port and protocol together with other information
to understand the connection.
</p>

<p>
<strong>Important:</strong> A port number alone does not prove which
application or attack is involved.
</p>

<hr>

<h2>17.3 Traffic Direction</h2>

<p>
<strong>Traffic Direction</strong> tells us where network traffic is moving.
</p>

<p><strong>Examples:</strong></p>

<pre>
Internal → External
External → Internal
Internal → Internal
</pre>

<h3>Internal → External</h3>

<p>This could be:</p>

<ul>
  <li>Normal web browsing</li>
  <li>Software updates</li>
  <li>Cloud services</li>
  <li>Malware communication</li>
  <li>Data exfiltration</li>
</ul>

<h3>External → Internal</h3>

<p>This could be:</p>

<ul>
  <li>Traffic to a public server</li>
  <li>VPN connection</li>
  <li>Remote access</li>
  <li>Attack attempt</li>
</ul>

<p>
Traffic direction gives useful context, but it does not by itself tell
us whether the activity is malicious.
</p>

<hr>

<h2>17.4 Client vs Server Identification</h2>

<p>
A <strong>Client</strong> normally requests a service, while a
<strong>Server</strong> normally provides that service.
</p>

<p><strong>Example:</strong></p>

<pre>
Employee Laptop → Web Server :443
</pre>

<p>
Here:
</p>

<pre>
Employee Laptop = Client
Web Server       = Server
</pre>

<p>
A SOC analyst should understand which system is acting as the client
and which system is acting as the server.
</p>

<p>
Unexpected behavior can be important. For example, if an employee
workstation suddenly starts accepting unusual incoming connections,
it may require investigation.
</p>

<hr>

<h2>17.5 Normal vs Suspicious Network Connections</h2>

<p>
Not every network connection is malicious.
</p>

<h3>Normal Examples</h3>

<pre>
User → DNS Server

User → Website :443

User → Email Server

Application Server → Database
</pre>

<h3>Potentially Suspicious Examples</h3>

<pre>
Workstation → Hundreds of Internal IPs

Server → Unknown External IP

Guest Device → Internal Server

One Host → Many Ports on Another Host
</pre>

<p>
Suspicious does <strong>not automatically mean malicious</strong>.
</p>

<p>
A SOC analyst needs to check whether the connection matches the
expected behavior of that system.
</p>

<hr>

<h2>17.6 Network Logs</h2>

<p>
<strong>Network Logs</strong> are records of network activity created by
systems, network devices, and security tools.
</p>

<p>They may contain:</p>

<ul>
  <li>Timestamp</li>
  <li>Source IP</li>
  <li>Destination IP</li>
  <li>Source Port</li>
  <li>Destination Port</li>
  <li>Protocol</li>
  <li>Action</li>
  <li>Bytes Transferred</li>
  <li>Connection Information</li>
</ul>

<p>
Network logs help a SOC analyst understand what happened between systems
and can help build a timeline during an investigation.
</p>

<hr>

<h2>17.7 Firewall Logs</h2>

<p>
<strong>Firewall Logs</strong> record network traffic observed, allowed,
or blocked by a firewall.
</p>

<p><strong>Example:</strong></p>

<pre>
SRC=192.168.1.25
DST=10.0.0.20
PROTO=TCP
DPT=22
ACTION=DENY
</pre>

<p>
From this log, an analyst can identify:
</p>

<pre>
Source      → 192.168.1.25
Destination → 10.0.0.20
Protocol    → TCP
Port        → 22
Action      → DENY
</pre>

<p>Firewall logs are useful when investigating:</p>

<ul>
  <li>Port Scanning</li>
  <li>Blocked Connections</li>
  <li>Unauthorized Access Attempts</li>
  <li>Suspicious Network Communication</li>
</ul>

<hr>

<h2>17.8 DNS Logs</h2>

<p>
<strong>DNS Logs</strong> contain information about domain-name lookups.
</p>

<p><strong>Example:</strong></p>

<pre>
Client: 192.168.1.25
Query:  example.com
Type:   A
</pre>

<p>A SOC analyst can use DNS logs to determine:</p>

<ul>
  <li>Which device requested the domain?</li>
  <li>Which domain was requested?</li>
  <li>When was it requested?</li>
  <li>What type of DNS query was made?</li>
  <li>Is the domain unusual or suspicious?</li>
</ul>

<p>
DNS logs can be useful because malware may use DNS when trying to locate
or communicate with external infrastructure.
</p>

<hr>

<h2>17.9 Proxy Logs</h2>

<p>
<strong>Proxy Logs</strong> record web activity that passes through a proxy.
</p>

<p>They may contain:</p>

<ul>
  <li>Username</li>
  <li>Source IP</li>
  <li>Domain</li>
  <li>URL</li>
  <li>HTTP Method</li>
  <li>Status</li>
  <li>Timestamp</li>
  <li>Allowed / Blocked Action</li>
</ul>

<p><strong>Example:</strong></p>

<pre>
User:    john
Source:  10.0.0.25
URL:     example.com
Method:  GET
Action:  ALLOW
</pre>

<p>
Proxy logs help a SOC analyst understand which websites or web resources
a user or device attempted to access.
</p>

<p>
They can be useful when investigating suspicious web activity or access
to unusual domains.
</p>

<hr>

<h2>17.10 VPN Logs</h2>

<p>
<strong>VPN Logs</strong> contain information about VPN connections and
remote-access activity.
</p>

<p>They may contain:</p>

<ul>
  <li>Username</li>
  <li>Public Source IP</li>
  <li>Login Time</li>
  <li>Authentication Result</li>
  <li>VPN-Assigned IP</li>
  <li>Session Duration</li>
</ul>

<p><strong>Example:</strong></p>

<pre>
User:       john
Source IP:  203.0.113.20
Result:     Success
VPN IP:     10.10.20.15
</pre>

<p>VPN logs can help investigate:</p>

<ul>
  <li>Repeated Failed Logins</li>
  <li>Successful Remote Access</li>
  <li>Unexpected Source IPs</li>
  <li>Unusual Login Times</li>
  <li>Suspicious Remote Connections</li>
</ul>

<hr>

<h2>17.11 Network Flow</h2>

<p>
<strong>Network Flow</strong> is a summary of communication between systems.
</p>

<p>
Instead of showing every individual packet, flow data can provide
important information about the overall connection.
</p>

<p><strong>Example:</strong></p>

<pre>
Source IP:         10.0.0.25
Destination IP:    10.0.0.50
Source Port:       51524
Destination Port:  443
Protocol:          TCP
Bytes:             25000
Duration:          8 seconds
</pre>

<p>
Network flow can help answer:
</p>

<blockquote>
Who communicated with whom, using which port and protocol, for how long,
and how much data was transferred?
</blockquote>

<p>
Flow data is useful for identifying unusual communication patterns
without inspecting every individual packet.
</p>

<hr>

<h2>17.12 Network Traffic Metadata</h2>

<p>
<strong>Network Traffic Metadata</strong> is information about network
communication without necessarily showing the actual content being transferred.
</p>

<p>Examples include:</p>

<ul>
  <li>Source IP</li>
  <li>Destination IP</li>
  <li>Source Port</li>
  <li>Destination Port</li>
  <li>Protocol</li>
  <li>Timestamp</li>
  <li>Duration</li>
  <li>Bytes Sent</li>
  <li>Bytes Received</li>
  <li>Connection State</li>
</ul>

<p>
Think about a phone call. You may know:
</p>

<pre>
Who called whom
When the call happened
How long the call lasted
</pre>

<p>
without knowing what the people actually said.
</p>

<p>
Network traffic metadata works in a similar way.
</p>

<p>
For SOC analysts, this information can be enough to identify unusual
communication patterns.
</p>

<hr>

<h2>17.13 Source &amp; Destination Relationship</h2>

<p>
A SOC analyst should not look at source and destination IP addresses
separately.
</p>

<p>
The analyst should also ask:
</p>

<blockquote>
Why are these two systems communicating?
</blockquote>

<h3>Example 1</h3>

<pre>
Employee PC → DNS Server
</pre>

<p>
This is normally expected.
</p>

<h3>Example 2</h3>

<pre>
Web Server → Database Server
</pre>

<p>
This may also be expected.
</p>

<h3>Example 3</h3>

<pre>
Guest Laptop → Domain Controller
</pre>

<p>
This may be unusual and require investigation.
</p>

<h3>Another Example</h3>

<pre>
Employee PC
    |
    +----→ Server 1
    |
    +----→ Server 2
    |
    +----→ Server 3
    |
    +----→ Server 4
    |
    +----→ Server 5
</pre>

<p>
A SOC analyst may investigate whether this activity is:
</p>

<ul>
  <li>Normal Application Activity</li>
  <li>Network Scanning</li>
  <li>Discovery Activity</li>
  <li>Possible Lateral Movement</li>
</ul>

<p>
<strong>Simple meaning:</strong><br>
Do not look at an IP address alone. Understand who is communicating
with whom, using which service, and whether that communication is expected.
</p>

<hr>

<h2>🎯 SOC L1 Perspective</h2>

<p>
When investigating network activity, a SOC L1 analyst should try to answer:
</p>

<pre>
Who started the connection?
          ↓
Who was the destination?
          ↓
Which port and protocol were used?
          ↓
What was the traffic direction?
          ↓
What do the network logs show?
          ↓
Is this communication expected?
          ↓
Normal or Suspicious?
</pre>

<p>
The main goal is not just to read IP addresses and ports.
</p>

<p>
<strong>
The goal is to connect all the network information together and
understand what actually happened.
</strong>
</p>
