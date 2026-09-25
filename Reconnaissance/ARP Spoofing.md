<h2>⚙️ Lab Setup & Baseline Verification</h2>

<p>
Before starting the ARP spoofing simulation, I verified the network configuration,
normal connectivity, web service and monitoring tools in the lab.
</p>

<h3>🖥️ Lab Environment</h3>

<table>
  <tr>
    <th>System</th>
    <th>Role</th>
    <th>IP Address</th>
    <th>Interface</th>
    <th>MAC Address</th>
  </tr>
  <tr>
    <td>Kali Linux</td>
    <td>Attacker</td>
    <td><code>192.168.67.129</code></td>
    <td><code>eth0</code></td>
    <td><code>00:0c:29:2e:03:d3</code></td>
  </tr>
  <tr>
    <td>Ubuntu Server</td>
    <td>Target Server</td>
    <td><code>192.168.67.128</code></td>
    <td><code>ens33</code></td>
    <td><code>00:0c:29:c1:0b:e4</code></td>
  </tr>
  <tr>
    <td>Ubuntu GUI</td>
    <td>Client / Victim</td>
    <td><code>192.168.67.130</code></td>
    <td><code>ens33</code></td>
    <td><code>00:0c:29:b3:d8:ab</code></td>
  </tr>
</table>
<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/c07c4931-8254-40cb-b770-9c69a1db70ab" />
<h2>⚔️ Attack Phase — ARP Spoofing / MITM</h2>

<p>
After completing the baseline checks, I started two-way ARP spoofing between
the Ubuntu GUI and Ubuntu Server. Wireshark remained active during the test.
</p>
<h3>🔁 Step 1 — Start Two-Way ARP Spoofing</h3>

<p>
Two separate Kali terminals were used because both sides of the communication
needed to be poisoned.
</p>
<blockquote>
  <strong>Finding:</strong><br>
  Kali continuously sent forged ARP replies in both directions. This created
  the required two-way ARP spoofing condition between the Ubuntu GUI and Server.
</blockquote>
<h3>🔍 Step 2 — Verify the ARP Table Change</h3>

<p>
After starting the attack, the ARP tables of both endpoints were checked to
confirm whether their original MAC mappings had changed.
</p>
<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/ff54cf46-d130-4207-a90f-793f4c1042f8" />
<h3>🔄 Step 3 — Verify MITM Forwarding</h3>

<p>
After confirming the ARP table changes, I tested whether the Ubuntu GUI could
still communicate with the Ubuntu Server through Kali.
</p>

<strong>Run on Ubuntu GUI: </strong>

```text
ping -c 4 192.168.67.128
```
<img width="781" height="447" alt="image" src="https://github.com/user-attachments/assets/e50752bf-4805-4d94-be7b-0458cfaab363" />
<h3>🌐 Step 4 — Generate HTTP Traffic</h3>

<p>
To generate application traffic during the MITM session, an HTTP request was
sent from the Ubuntu GUI to DVWA.
</p>
<strong>Run on Ubuntu GUI: </strong>

```text 
curl -v --max-time 5 http://192.168.67.128/dvwa/ -o /dev/null
```
<img width="1342" height="555" alt="image" src="https://github.com/user-attachments/assets/8fd26a9a-4348-4daa-b825-4687bc4aef98" />
<blockquote>
  <strong>Finding:</strong><br>
  The Ubuntu GUI successfully accessed DVWA over unencrypted HTTP while the
  MITM session was active. The request and server response were generated for
  packet-capture verification.
</blockquote>
<h5>🔍 Wireshark Verification</h5>

```text
http && ip.addr == 192.168.67.130 && ip.addr == 192.168.67.128
```
<img width="1357" height="517" alt="image" src="https://github.com/user-attachments/assets/1b978c6e-4eb2-4213-b407-aaa51255ba87" />

<blockquote>
  <strong>Finding:</strong><br>
  Kali Wireshark observed the <code>GET /dvwa/</code> request and
  <code>302 Found</code> response, confirming that the HTTP traffic passed
  through Kali during the lab session.
</blockquote>
<hr>
<h2>🔎 Investigation Phase</h2>
<p>
After completing the ARP spoofing / MITM simulation, I reviewed the SOC dashboard
to identify the security events generated during the activity.
</p>

<p>
Suricata IDS recorded network alerts during the test period, while no UFW firewall
events were observed. Since ARP spoofing operates at the local network layer,
packet-level evidence is also important for validating the activity.
</p>
<img width="1839" height="723" alt="image" src="https://github.com/user-attachments/assets/06c605b7-7516-44a3-a144-1927841d6de5" />

<h3>📌 Initial Observations</h3>

<ul>
  <li>🛡️ <strong>Suricata IDS</strong> generated multiple <code>GPL ICMP_INFO PING *NIX</code> alerts.</li>
  <li>🌐 <strong>DVWA web activity</strong> was available during the same investigation period.</li>
  <li>🔥 <strong>UFW Firewall</strong> did not record any related events.</li>
  <li>📦 Packet-level evidence will be reviewed to validate the ARP spoofing / MITM activity.</li>
</ul>

<blockquote>
<b>Note:</b> ARP spoofing is a Layer 2 network activity, so firewall logs may not
directly record the poisoning activity. IDS alerts and packet captures are more
useful for validating this type of incident.
</blockquote>

<h3>🚨 Step 1 — Alert Triage & Scope</h3>

<p>
The first step of the investigation was to review the Suricata alerts and understand
what activity was detected. Before checking deeper logs or packet captures, I first
identified the source, destination, protocol, alert signature and number of events.
This helped define the initial scope of the incident.
</p>


<h4>1. Initial Alert Summary</h4>

<h6>SOC L1 Thinking</h6>

<blockquote>
I saw Suricata alerts on the dashboard, but I did not yet know what activity
they represented. So I reviewed the alert details to get the basic picture of
what was detected, which hosts were involved, what protocol was used, and how
often the alert occurred.
</blockquote>

<pre><code>index=soc_network sourcetype=suricata event_type=alert
| stats count BY src_ip dest_ip proto alert.signature
| sort - count
</code></pre>

<img width="1287" height="371" alt="image" src="https://github.com/user-attachments/assets/ad1fc724-5a85-42e3-b1a2-64ba62ac7d55" />
<blockquote>
<strong>Finding:</strong><br>
Suricata detected 22 ICMP ping alerts from
<code>192.168.67.130</code> to <code>192.168.67.128</code>.
This confirmed that repeated ICMP communication was present between the two systems.
</blockquote>

<h4>2. Timeline & Duration</h4>
<h6>SOC L1 Thinking</h6>

<blockquote>
After identifying the alert, I now know the source, destination and type of activity. Next, I wanted to check
when the alerts started, when they stopped, and how long the activity continued.
</blockquote>

<pre><code>index=soc_network sourcetype=suricata event_type=alert
src_ip="192.168.67.130" dest_ip="192.168.67.128"
"alert.signature"="GPL ICMP_INFO PING *NIX"
| stats count AS alert_count
        earliest(_time) AS first_seen
        latest(_time) AS last_seen
| eval duration_minutes=round((last_seen-first_seen)/60,2)
| convert ctime(first_seen) ctime(last_seen)
</code></pre>
<img width="1282" height="486" alt="image" src="https://github.com/user-attachments/assets/fc868ece-c6ee-4ceb-95e9-2e51d952c579" />
<blockquote>
<strong>Finding:</strong><br>
The 22 ICMP alerts were observed across an approximately
<strong>22.61-minute</strong> time window.
</blockquote>

<h4>3. Alert Pattern Review</h4>

<h6>SOC L1 Thinking</h6>

<blockquote>
I found that the activity lasted for around 22.61 minutes, but I still needed to understand
how the alerts were occurring during that time. So, I reviewed the timestamps of the
individual alerts to see how the activity was distributed.
</blockquote>
<pre><code>index=soc_network sourcetype=suricata event_type=alert
src_ip="192.168.67.130" dest_ip="192.168.67.128"
"alert.signature"="GPL ICMP_INFO PING *NIX"
| table _time src_ip dest_ip proto alert.signature
| sort _time
</code></pre>
<img width="1280" height="482" alt="image" src="https://github.com/user-attachments/assets/b04e4531-7e3e-4adc-b616-52ef9f2418a9" />
<blockquote>
<strong>Finding:</strong><br>
The alerts appeared at multiple timestamps during the observed activity window,
showing repeated ICMP activity rather than a single isolated event.
</blockquote>

<blockquote>
<strong>🔎 Step 1 Finding:</strong><br>
The initial triage identified 22 ICMP alerts from
<code>192.168.67.130</code> to <code>192.168.67.128</code>
over approximately <strong>22.61 minutes</strong>.
The alerts confirm repeated ICMP communication between the two systems.
Further log and packet analysis is required to determine whether this activity
is related to the ARP spoofing / MITM simulation.
</blockquote>
<h3>🔎 Step 2 — Relevant Log Analysis</h3>
<h4>1. Identify Relevant Event Types</h4>
<h6>SOC L1 Thinking</h6>

<blockquote>
After reviewing the initial alerts, The ICMP alerts showed repeated communication between the two hosts, but they
did not provide enough context about the overall activity. So I checked the
other Suricata event types to see what additional network activity was recorded
between these hosts.
</blockquote>

<h5>🔍 Splunk Query</h5>

<pre><code>index=soc_network sourcetype=suricata
src_ip="192.168.67.130" dest_ip="192.168.67.128"
event_type IN (alert, flow, http)
| stats count BY event_type
| sort - count
</code></pre>
<img width="1283" height="414" alt="image" src="https://github.com/user-attachments/assets/89ae72bd-51a9-46f1-a086-06b7eb7b62a7" />

<blockquote>
<strong>Finding:</strong><br>
The selected traffic contained 31 Suricata events across alert, flow and HTTP
event types. This showed that the communication between the two hosts included
additional network activity beyond the ICMP alerts identified during triage.
</blockquote>
<h4>2. HTTP Events Analysis</h4>
<h6>SOC L1 Thinking</h6>

<blockquote>
The previous finding showed that HTTP events were also present between the same
two hosts. So, I checked the HTTP requests to understand what web communication
was taking place during the observed activity by reviewing the HTTP method,
requested URL, response status and redirect information.
</blockquote>
<p><strong>Query:</strong></p>

<pre><code>index=soc_network sourcetype=suricata
src_ip="192.168.67.130" dest_ip="192.168.67.128"
event_type=http
| table _time http.http_method http.url http.status http.redirect
| sort _time</code></pre>

<img width="1280" height="397" alt="image" src="https://github.com/user-attachments/assets/5c280e7a-ccdf-428f-93ee-6f0adf034ea4" />

<h5>Findings</h5>

<ul>
  <li>2 HTTP GET requests to <code>/dvwa/</code> were observed.</li>
  <li>Both requests returned <code>302</code> and redirected to <code>login.php</code>.</li>
  <li>User-Agent: <code>curl/7.81.0</code>.</li>
</ul>

<p>
  <strong>L1 Assessment:</strong>
  The logs confirmed ICMP and HTTP activity between the two hosts, but they did
not explain the cause of the observed communication. I therefore needed
packet-level evidence to investigate whether any abnormal ARP activity was
present.
</p>
