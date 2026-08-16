<h1>Chapter 14 — Packets &amp; Network Traffic</h1>
<img width="800" height="1200" alt="image" src="https://github.com/user-attachments/assets/0e2b1f60-c404-484c-a762-da0d8ac6f135" />

<p>
Network communication is divided into different data units as information
moves through different layers of the network.
Understanding packets, frames, headers, and traffic is important for
network troubleshooting and SOC investigations.
</p>

<hr>

<h2>14.1 Packet</h2>

<p>
A <strong>packet</strong> is a unit of network-layer data used to carry
information from one IP address to another.
</p>

<p>A packet normally contains:</p>

<ul>
  <li>Source IP</li>
  <li>Destination IP</li>
  <li>Protocol information</li>
  <li>Data</li>
</ul>

<p>
<strong>Simple meaning:</strong><br>
Packet = Data being carried across an IP network.
</p>

<hr>

<h2>14.2 Frame</h2>

<p>
A <strong>frame</strong> is the data unit used at the
<strong>Data Link Layer</strong>.
</p>

<p>
Frames are used for communication on a local network, such as between
a computer and a switch.
</p>

<p>A frame commonly contains:</p>

<ul>
  <li>Source MAC Address</li>
  <li>Destination MAC Address</li>
  <li>Payload</li>
  <li>Ethernet Information</li>
</ul>

<p>
<strong>Simple meaning:</strong><br>
Frame = Data carried across the local Ethernet network.
</p>

<hr>

<h2>14.3 Segment</h2>

<p>
A <strong>segment</strong> is commonly used to describe TCP data at the
<strong>Transport Layer</strong>.
</p>

<p>It can contain:</p>

<ul>
  <li>Source Port</li>
  <li>Destination Port</li>
  <li>TCP Flags</li>
  <li>Sequence Information</li>
  <li>Application Data</li>
</ul>

<p>
For UDP, the transport-layer data unit is normally called a
<strong>datagram</strong>, not a segment.
</p>

<p>
<strong>TCP → Segment</strong><br>
<strong>UDP → Datagram</strong>
</p>

<hr>

<h2>14.4 Packet Headers</h2>

<p>
A <strong>header</strong> contains control and addressing information
added to network data.
</p>

<p>Headers help devices understand:</p>

<ul>
  <li>Where the data came from</li>
  <li>Where it is going</li>
  <li>Which protocol is being used</li>
  <li>How the data should be handled</li>
</ul>

<p>
Different network layers add different headers.
</p>

<hr>

<h2>14.5 IP Header</h2>

<p>
The <strong>IP Header</strong> contains information needed for IP
communication.
</p>

<p>Important fields include:</p>

<ul>
  <li>Source IP Address</li>
  <li>Destination IP Address</li>
  <li>Protocol</li>
  <li>TTL / Hop Limit</li>
  <li>Packet Length</li>
</ul>

<h3>Example</h3>

<pre>
Source IP      → 10.10.1.25
Destination IP → 10.10.1.50
Protocol       → TCP
</pre>

<p>
For SOC analysis, <strong>Source and Destination IPs</strong> are
especially important.
</p>

<hr>

<h2>14.6 TCP Header</h2>

<p>
The <strong>TCP Header</strong> contains information used to establish
and manage TCP communication.
</p>

<p>Important fields include:</p>

<ul>
  <li>Source Port</li>
  <li>Destination Port</li>
  <li>Sequence Number</li>
  <li>Acknowledgment Number</li>
  <li>TCP Flags</li>
  <li>Window Information</li>
</ul>

<h3>Common TCP Flags</h3>

<pre>
SYN
ACK
FIN
RST
PSH
URG
</pre>

<p>
TCP flags can help an analyst understand the state and behavior of
a TCP connection.
</p>

<hr>

<h2>14.7 UDP Header</h2>

<p>
The <strong>UDP Header</strong> is simpler than the TCP Header.
</p>

<p>Important fields include:</p>

<ul>
  <li>Source Port</li>
  <li>Destination Port</li>
  <li>Length</li>
  <li>Checksum</li>
</ul>

<p>
UDP does not provide TCP-style connection management or a
3-way handshake.
</p>

<p>UDP is commonly used by protocols such as:</p>

<ul>
  <li>DNS</li>
  <li>DHCP</li>
  <li>NTP</li>
</ul>

<hr>

<h2>14.8 Ethernet Header</h2>

<p>
The <strong>Ethernet Header</strong> is used for communication on
an Ethernet network.
</p>

<p>Important information includes:</p>

<ul>
  <li>Source MAC</li>
  <li>Destination MAC</li>
  <li>EtherType</li>
</ul>

<h3>Example</h3>

<pre>
Source MAC      → AA:BB:CC:11:22:33
Destination MAC → DD:EE:FF:44:55:66
</pre>

<p>
<strong>Important difference:</strong>
</p>

<p>
IP addresses help identify hosts at the network layer.
<br>
MAC addresses identify interfaces on the local Ethernet network.
</p>

<hr>

<h2>14.9 Source &amp; Destination</h2>

<p>
Network traffic normally contains <strong>Source</strong> and
<strong>Destination</strong> information.
</p>

<h3>Example</h3>

<pre>
Source      → 10.10.1.25
Destination → 8.8.8.8
</pre>

<p>
At different layers, you may see:
</p>

<ul>
  <li>Source / Destination MAC</li>
  <li>Source / Destination IP</li>
  <li>Source / Destination Port</li>
</ul>

<p>
For SOC L1, these are extremely important because they help answer:
</p>

<blockquote>
  <strong>Who communicated with whom?</strong>
</blockquote>

<hr>

<h2>14.10 Packet Flow</h2>

<p>
<strong>Packet flow</strong> describes how network data moves between
systems.
</p>

<p>
Traffic may travel through network devices such as switches and routers.
</p>

<pre>
Client → Switch → Router → Server
</pre>

<p>
Outbound traffic travels toward the destination, while response traffic
comes back toward the original client.
</p>

<p>
During an investigation, an analyst may examine
<strong>both directions</strong> of the communication.
</p>

<hr>

<h2>14.11 Normal Network Traffic</h2>

<p>
Not all network traffic is malicious.
</p>

<p>Normal traffic can include:</p>

<ul>
  <li>DNS Queries</li>
  <li>Web Browsing</li>
  <li>Email</li>
  <li>Software Updates</li>
  <li>DHCP Communication</li>
  <li>File Sharing</li>
  <li>Time Synchronization</li>
</ul>

<p>
A SOC analyst needs to understand <strong>normal behavior</strong>
before identifying unusual behavior.
</p>

<h3>Example</h3>

<pre>
User PC → DNS Server
User PC → Web Server
User PC → Email Server
</pre>

<p>
These may all be completely normal depending on the environment.
</p>

<hr>

<h2>14.12 Wireshark Basics</h2>

<p>
<strong>Wireshark</strong> is a network protocol analyzer used to capture
and inspect network traffic.
</p>

<p>It allows you to examine:</p>

<ul>
  <li>Packets</li>
  <li>Protocols</li>
  <li>IP Addresses</li>
  <li>MAC Addresses</li>
  <li>Ports</li>
  <li>TCP Flags</li>
  <li>DNS Requests</li>
  <li>HTTP Traffic</li>
  <li>Packet Details</li>
</ul>

<h3>Example Display Filters</h3>

<pre>
ip.addr == 10.10.1.25
</pre>

<p>
Filters traffic involving the specified IP address.
</p>

<pre>
tcp.port == 443
</pre>

<p>
Filters TCP traffic using port 443.
</p>

<h3>SOC L1 Use</h3>

<p>Wireshark can help answer questions such as:</p>

<ul>
  <li>Which IP communicated with the host?</li>
  <li>Which port was used?</li>
  <li>Which protocol was involved?</li>
  <li>Was the connection TCP or UDP?</li>
  <li>What TCP flags were observed?</li>
  <li>What happened during the packet exchange?</li>
</ul>

<hr>

<h2>🧠 Data Units Quick Revision</h2>

<table>
  <thead>
    <tr>
      <th>Layer / Protocol</th>
      <th>Data Unit</th>
      <th>Important Information</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Ethernet / Data Link</td>
      <td><strong>Frame</strong></td>
      <td>MAC Addresses</td>
    </tr>
    <tr>
      <td>IP / Network</td>
      <td><strong>Packet</strong></td>
      <td>IP Addresses</td>
    </tr>
    <tr>
      <td>TCP / Transport</td>
      <td><strong>Segment</strong></td>
      <td>Ports, Flags, Sequence Information</td>
    </tr>
    <tr>
      <td>UDP / Transport</td>
      <td><strong>Datagram</strong></td>
      <td>Ports, Length, Checksum</td>
    </tr>
  </tbody>
</table>

<hr>

<h2>🎯 SOC L1 Perspective</h2>

<p>
Packet information helps a SOC analyst connect different pieces of
network activity.
</p>

<pre>
Source IP
    ↓
Destination IP
    ↓
Port
    ↓
Protocol
    ↓
Packet / Frame Details
</pre>

<p>
This helps the analyst understand:
</p>

<ul>
  <li>What communicated?</li>
  <li>Where did it go?</li>
  <li>Which protocol was used?</li>
  <li>Which port was involved?</li>
  <li>How did the communication behave?</li>
</ul>

<p>
<strong>
Understanding packet and traffic details provides a clearer picture
of network communication during SOC investigations.
</strong>
</p>
