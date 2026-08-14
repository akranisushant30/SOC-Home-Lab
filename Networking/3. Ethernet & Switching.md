<h1>Chapter 3 — Ethernet &amp; Switching</h1>
<img width="800" height="1200" alt="image" src="https://github.com/user-attachments/assets/a542b889-bb00-4cbc-8af1-02990199bce8" />

<h2>1. Ethernet</h2>

<p>
<strong>Ethernet</strong> is a technology used for communication between devices in a <strong>LAN</strong>.
</p>

<p><strong>Example:</strong></p>

<pre>
PC → Ethernet Cable → Switch
</pre>

<p>
It defines how data is sent over a local network and uses <strong>MAC addresses</strong> for local communication.
</p>

<hr>

<h2>2. MAC Address</h2>

<p>
A <strong>MAC address</strong> is an address associated with a network interface.
</p>

<p><strong>Example:</strong></p>

<pre>
A4:5E:60:12:AB:9F
</pre>

<p>
It helps identify a device's network interface on the local network.
</p>

<p><strong>Easy Difference:</strong></p>

<ul>
  <li><strong>IP Address</strong> → Logical address used to locate a device/network</li>
  <li><strong>MAC Address</strong> → Used for local network communication</li>
</ul>

<hr>

<h2>3. NIC</h2>

<p>
<strong>NIC = Network Interface Card/Controller</strong>
</p>

<p>
A NIC allows a device to connect to a network.
</p>

<p>Examples:</p>

<ul>
  <li>Wi-Fi NIC</li>
  <li>Ethernet NIC</li>
</ul>

<p>
The NIC has a <strong>MAC address</strong>.
</p>

<p>
Think of the NIC as your computer's <strong>network connection interface</strong>.
</p>

<hr>

<h2>4. Frames</h2>

<p>
A <strong>frame</strong> is the data unit used at the Ethernet/Data Link layer.
</p>

<p>A simplified frame contains:</p>

<ul>
  <li><strong>Source MAC</strong></li>
  <li><strong>Destination MAC</strong></li>
  <li><strong>Data</strong></li>
  <li><strong>Error-checking information</strong></li>
</ul>

<p>
The switch mainly looks at the <strong>destination MAC</strong> to decide where to send the frame.
</p>

<hr>

<h2>5. Switch</h2>

<p>
A <strong>switch</strong> connects multiple devices inside a LAN.
</p>

<p><strong>Example:</strong></p>

<pre>
PC → Switch ← Server
</pre>

<p>
The switch checks the destination MAC address and forwards the frame toward the correct port.
</p>

<p>
<strong>Switch = Connects devices within a LAN.</strong>
</p>

<hr>

<h2>6. MAC Address Table</h2>

<p>
A switch maintains a table that tells it <strong>which MAC address is connected to which port</strong>.
</p>

<table>
  <thead>
    <tr>
      <th>MAC Address</th>
      <th>Port</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>AA:AA:AA:01</td>
      <td>Port 1</td>
    </tr>
    <tr>
      <td>BB:BB:BB:02</td>
      <td>Port 2</td>
    </tr>
  </tbody>
</table>

<p>
The switch learns these MAC addresses from incoming frames.
</p>

<hr>

<h2>7. Unicast, Broadcast &amp; Multicast</h2>

<p>
These describe how network traffic is delivered.
</p>

<h3>Unicast</h3>

<p><strong>One → One</strong></p>

<pre>
PC A → PC B
</pre>

<h3>Broadcast</h3>

<p><strong>One → Everyone on the local broadcast domain</strong></p>

<pre>
PC A → All
</pre>

<h3>Multicast</h3>

<p><strong>One → Selected Group</strong></p>

<pre>
Server → Specific Group
</pre>

<p>
ARP requests are a common example of <strong>broadcast traffic</strong> in IPv4 LANs.
</p>

<hr>

<h2>8. ARP</h2>

<p>
<strong>ARP = Address Resolution Protocol</strong>
</p>

<p>
ARP helps find the <strong>MAC address when a device knows the IPv4 address</strong>.
</p>

<p><strong>Example:</strong></p>

<p>
Your PC knows:
</p>

<pre>
192.168.1.20
</pre>

<p>
But it doesn't know the MAC address.
</p>

<p>
It asks:
</p>

<blockquote>
"Who has 192.168.1.20?"
</blockquote>

<p>
The device with that IP replies with its MAC address.
</p>

<p>
<strong>ARP = IPv4 Address → MAC Address</strong>
</p>

<hr>

<h2>9. ARP Cache</h2>

<p>
The computer temporarily stores learned <strong>IP-to-MAC mappings</strong> in its ARP cache.
</p>

<p><strong>Example:</strong></p>

<pre>
192.168.1.20 → AA:BB:CC:DD:EE:FF
</pre>

<p>
This avoids sending a new ARP request every time.
</p>

<p>
<strong>SOC Relevance:</strong> ARP can be abused in <strong>ARP spoofing/poisoning attacks</strong>.
</p>

<hr>

<h2>10. VLAN Basics</h2>

<p>
<strong>VLAN = Virtual Local Area Network</strong>
</p>

<p>
A VLAN logically separates devices into different networks.
</p>

<p><strong>Example:</strong></p>

<pre>
VLAN 10 → HR
VLAN 20 → IT
VLAN 30 → Guest
</pre>

<p>
Even if these devices use the same physical switch, VLANs can keep their traffic logically separated.
</p>

<h3>Why VLANs?</h3>

<ul>
  <li>Security</li>
  <li>Segmentation</li>
  <li>Network Management</li>
</ul>

<hr>

<h2>Chapter 3 — Key Concepts</h2>

<pre>
Ethernet
   ↓
MAC Address
   ↓
Frames
   ↓
Switch
   ↓
MAC Address Table
   ↓
ARP
   ↓
VLAN
</pre>

<p>
These concepts help you understand how devices communicate inside a local network and how switching works.
</p>
