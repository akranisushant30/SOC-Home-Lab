<h1>Chapter 10 — Firewalls &amp; Network Security Devices</h1>
<img width="800" height="1200" alt="image" src="https://github.com/user-attachments/assets/7b9cf52b-ef7f-467d-86fe-89336b1d5644" />

<p>
A <strong>firewall</strong> and other network security devices help control,
inspect, detect, and protect network traffic.
</p>

<hr>

<h2>1. Firewall Basics</h2>

<p>
A <strong>firewall</strong> is a security device or software that controls
network traffic based on defined rules.
</p>

<p>
A firewall can decide whether traffic should be:
</p>

<ul>
  <li><strong>Allowed</strong></li>
  <li><strong>Blocked</strong></li>
</ul>

<p>
A firewall can inspect information such as:
</p>

<ul>
  <li>Source IP</li>
  <li>Destination IP</li>
  <li>Port</li>
  <li>Protocol</li>
  <li>Connection state</li>
</ul>

<p>
<strong>Simple meaning:</strong>
Firewall = A security gate that controls network traffic.
</p>

<hr>

<h2>2. Stateful &amp; Stateless Firewall</h2>

<h3>Stateless Firewall</h3>

<p>
A <strong>stateless firewall</strong> checks each packet independently.
</p>

<p>
It mainly looks at:
</p>

<ul>
  <li>Source IP</li>
  <li>Destination IP</li>
  <li>Port</li>
  <li>Protocol</li>
</ul>

<p>
It does not keep track of the connection state.
</p>

<h3>Stateful Firewall</h3>

<p>
A <strong>stateful firewall</strong> keeps track of active connections.
</p>

<p>
For example, it can understand that a packet belongs to an already-established
TCP connection.
</p>

<p>
<strong>Stateless → Checks individual packets</strong><br>
<strong>Stateful → Tracks connection state</strong>
</p>

<hr>

<h2>3. Firewall Rules</h2>

<p>
A firewall uses <strong>rules</strong> to decide what traffic is allowed
or blocked.
</p>

<p>A rule can contain:</p>

<pre>
Source
Destination
Protocol
Port
Action
</pre>

<p>Example:</p>

<pre>
Source:      Any
Destination: Web Server
Protocol:    TCP
Port:        443
Action:      Allow
</pre>

<p>
This rule allows HTTPS traffic to the web server.
</p>

<hr>

<h2>4. Allow &amp; Deny</h2>

<h3>Allow</h3>

<p>
The firewall permits traffic that matches the rule.
</p>

<pre>
TCP 443 → ALLOW
</pre>

<h3>Deny</h3>

<p>
The firewall blocks traffic that matches the rule.
</p>

<pre>
TCP 23 → DENY
</pre>

<p>
Depending on the firewall, actions may include:
</p>

<ul>
  <li>Allow</li>
  <li>Deny</li>
  <li>Reject</li>
  <li>Drop</li>
</ul>

<p>
The exact behavior of <strong>deny, reject, and drop</strong> can vary
depending on the firewall.
</p>

<hr>

<h2>5. Inbound &amp; Outbound Traffic</h2>

<h3>Inbound Traffic</h3>

<p>
<strong>Inbound traffic</strong> is traffic coming into a network or system.
</p>

<pre>
Internet → Internal Server
</pre>

<p>
A firewall can control which external systems are allowed to reach
internal services.
</p>

<h3>Outbound Traffic</h3>

<p>
<strong>Outbound traffic</strong> is traffic leaving a network or system.
</p>

<pre>
Internal Computer → Internet
</pre>

<p>
Outbound rules can control where internal systems are allowed to connect.
</p>

<p>
<strong>Inbound = Coming in</strong><br>
<strong>Outbound = Going out</strong>
</p>

<hr>

<h2>6. Source &amp; Destination</h2>

<p>
Every network connection has a <strong>source</strong> and a
<strong>destination</strong>.
</p>

<h3>Source</h3>

<p>
The device that sends or starts the traffic.
</p>

<h3>Destination</h3>

<p>
The device that receives the traffic.
</p>

<pre>
Source:      192.168.1.50
Destination: 192.168.1.10
</pre>

<p>
Here:
</p>

<ul>
  <li><code>192.168.1.50</code> = Source</li>
  <li><code>192.168.1.10</code> = Destination</li>
</ul>

<p>
Firewall rules use these values to control traffic.
</p>

<hr>

<h2>7. Ports &amp; Protocols in Rules</h2>

<p>
Firewalls can control traffic based on <strong>protocol and port</strong>.
</p>

<p>Example:</p>

<pre>
Protocol: TCP
Port: 443
Action: ALLOW
</pre>

<p>
This commonly represents HTTPS traffic.
</p>

<p>Another example:</p>

<pre>
Protocol: TCP
Port: 22
Action: ALLOW
</pre>

<p>
This allows SSH traffic.
</p>

<p>
Understanding <strong>ports + protocols</strong> is important when
working with firewall rules and logs.
</p>

<hr>

<h2>8. ACL — Access Control List</h2>

<p>
An <strong>ACL</strong> is a list of rules used to control network traffic.
</p>

<p>An ACL can specify:</p>

<ul>
  <li>Source</li>
  <li>Destination</li>
  <li>Protocol</li>
  <li>Port</li>
  <li>Allow / Deny</li>
</ul>

<p>Example:</p>

<pre>
ALLOW  192.168.1.0/24 → Server
DENY   Any → Server:23
</pre>

<p>
ACLs can be used on:
</p>

<ul>
  <li>Routers</li>
  <li>Firewalls</li>
  <li>Switches</li>
  <li>Network security devices</li>
</ul>

<p>
<strong>Simple meaning:</strong>
ACL = A list of traffic-control rules.
</p>

<hr>

<h2>9. Proxy</h2>

<p>
A <strong>proxy</strong> acts as an intermediary between a client and
another server.
</p>

<p>
Instead of the client communicating directly with the destination,
the proxy handles the request on its behalf.
</p>

<pre>
Client → Proxy → Website
</pre>

<p>Proxies can be used for:</p>

<ul>
  <li>Web filtering</li>
  <li>Access control</li>
  <li>Logging</li>
  <li>Caching</li>
  <li>Controlling outbound web access</li>
</ul>

<p>
A <strong>forward proxy</strong> is commonly used to control outbound
web access from internal users.
</p>

<hr>

<h2>10. IDS &amp; IPS</h2>

<h3>IDS — Intrusion Detection System</h3>

<p>
An <strong>IDS</strong> monitors network activity and detects suspicious
or malicious behavior.
</p>

<p>
When suspicious activity is detected, an IDS can generate an alert.
</p>

<pre>
Suspicious Traffic → IDS → ALERT
</pre>

<p>
<strong>IDS = Detection and Alerting</strong>
</p>

<h3>IPS — Intrusion Prevention System</h3>

<p>
An <strong>IPS</strong> can detect suspicious traffic and actively block it.
</p>

<pre>
Suspicious Traffic → IPS → BLOCK
</pre>

<p>
<strong>IPS = Detection + Prevention</strong>
</p>

<h3>Simple Difference</h3>

<table>
  <thead>
    <tr>
      <th>IDS</th>
      <th>IPS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Detects suspicious activity</td>
      <td>Detects suspicious activity</td>
    </tr>
    <tr>
      <td>Generates alerts</td>
      <td>Can block suspicious traffic</td>
    </tr>
  </tbody>
</table>

<hr>

<h2>11. WAF — Web Application Firewall</h2>

<p>
A <strong>WAF</strong> is designed specifically to protect
<strong>web applications</strong>.
</p>

<p>
It examines HTTP/HTTPS traffic and can help detect or block attacks such as:
</p>

<ul>
  <li>SQL Injection</li>
  <li>Cross-Site Scripting (XSS)</li>
  <li>Malicious HTTP requests</li>
</ul>

<pre>
Internet
   ↓
  WAF
   ↓
Web Application
</pre>

<h3>Firewall vs WAF</h3>

<p>
<strong>Firewall → General network traffic</strong><br>
<strong>WAF → Web application traffic</strong>
</p>

<hr>

<h2>12. VPN — Virtual Private Network</h2>

<p>
A <strong>VPN</strong> creates an encrypted connection between devices
or networks over an untrusted network such as the Internet.
</p>

<p>
For example, an employee working remotely can connect to the company's
internal network through a VPN.
</p>

<pre>
Employee → Internet → VPN → Company Network
</pre>

<p>VPNs are commonly used for:</p>

<ul>
  <li>Remote access</li>
  <li>Site-to-site connections</li>
  <li>Secure communication over public networks</li>
</ul>

<p>
<strong>Simple meaning:</strong>
VPN = Secure encrypted connection over an untrusted network.
</p>

<hr>

<h2>13. Security Zones</h2>

<p>
A network can be divided into different <strong>security zones</strong>
based on trust level and security requirements.
</p>

<h3>Internet / Untrusted Zone</h3>

<p>
Public networks that are generally treated as untrusted.
</p>

<h3>DMZ — Demilitarized Zone</h3>

<p>
A DMZ is a network segment used for systems that need to be reachable
from external networks.
</p>

<p>
Example:
</p>

<ul>
  <li>Public Web Server</li>
  <li>Public Mail Server</li>
</ul>

<h3>Internal / Trusted Zone</h3>

<p>
Contains internal systems and users.
</p>

<h3>Restricted Zone</h3>

<p>
Contains highly sensitive systems that require stronger access controls.
</p>

<p>
<strong>Security zones help organizations separate systems according
to their exposure and security requirements.</strong>
</p>

<hr>

<h2>🎯 SOC L1 Connection</h2>

<p>
Firewall logs are important evidence during security investigations.
They can help answer:
</p>

<ul>
  <li>Who communicated with whom?</li>
  <li>What protocol and port were used?</li>
  <li>Was the traffic inbound or outbound?</li>
  <li>Was the traffic allowed or blocked?</li>
  <li>When did the connection occur?</li>
</ul>

<h3>Example — Allowed Traffic</h3>

<pre>
Source:      10.10.1.50
Destination: 8.8.8.8
Protocol:    TCP
Port:        443
Action:      ALLOW
</pre>

<p>
This indicates an allowed HTTPS connection from the internal host
to the destination.
</p>

<h3>Example — Blocked Traffic</h3>

<pre>
Source:      10.10.1.50
Destination: Suspicious IP
Protocol:    TCP
Port:        4444
Action:      DENY
</pre>

<p>
Repeated attempts to connect to a suspicious destination or unusual port
can become important during an investigation.
</p>

<p>
<strong>
For SOC L1, understanding firewall logs means connecting
Source IP + Destination IP + Port + Protocol + Direction + Action.
</strong>
</p>
