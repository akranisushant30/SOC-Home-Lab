<h1>Chapter 2 — OSI &amp; TCP/IP Models</h1>
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/df17f274-f45c-44f5-a67d-89cbedbd5969" />
<h2>1. OSI Model</h2>

<p>
The <strong>OSI Model</strong> is a framework that explains how data moves from one device to another.
</p>

<p>It has <strong>7 layers</strong>:</p>

<pre>
7. Application
6. Presentation
5. Session
4. Transport
3. Network
2. Data Link
1. Physical
</pre>

<p>
Think of it like <strong>7 steps in a delivery process</strong>. When you open a website, data passes through these layers while moving between your computer and the server.
</p>

<p>
<strong>SOC Perspective:</strong> The OSI model helps analysts understand where a network problem or attack is happening.
</p>

<hr>

<h2>2. TCP/IP Model</h2>

<p>
The <strong>TCP/IP Model</strong> is the practical model used by modern networks and the Internet.
</p>

<p>It usually has <strong>4 layers</strong>:</p>

<pre>
4. Application
3. Transport
2. Internet
1. Network Access
</pre>

<table>
  <thead>
    <tr>
      <th>Layer</th>
      <th>Examples</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Application</strong></td>
      <td>HTTP, DNS, SSH</td>
    </tr>
    <tr>
      <td><strong>Transport</strong></td>
      <td>TCP, UDP</td>
    </tr>
    <tr>
      <td><strong>Internet</strong></td>
      <td>IP</td>
    </tr>
    <tr>
      <td><strong>Network Access</strong></td>
      <td>Ethernet, Wi-Fi</td>
    </tr>
  </tbody>
</table>

<p>
Think of TCP/IP as the <strong>real-world model used for networking</strong>, while OSI is mainly used to understand networking concepts.
</p>

<hr>

<h2>3. OSI vs TCP/IP</h2>

<p>
The main difference is the number of layers and how they are organized.
</p>

<pre>
OSI Model              TCP/IP Model

Application  ┐
Presentation ├──────→  Application
Session      ┘

Transport    ───────→  Transport

Network      ───────→  Internet

Data Link    ┐
Physical     ┘──────→  Network Access
</pre>

<h3>Easy Difference</h3>

<ul>
  <li><strong>OSI</strong> → 7-layer learning/reference model</li>
  <li><strong>TCP/IP</strong> → Practical model used for Internet communication</li>
</ul>

<hr>

<h2>4. Encapsulation &amp; Decapsulation</h2>

<h3>Encapsulation</h3>

<p>
When you send data, each networking layer <strong>adds its own information</strong> to the data.
</p>

<p>Think of it like sending a parcel:</p>

<pre>
Your Data
   ↓
Put inside a package
   ↓
Add address
   ↓
Add shipping information
   ↓
Send it
</pre>

<p>In networking:</p>

<pre>
Data
 ↓
Segment
 ↓
Packet
 ↓
Frame
 ↓
Bits
</pre>

<h3>Decapsulation</h3>

<p>
When the receiving computer gets the data, it <strong>removes the information step by step</strong>.
</p>

<pre>
Bits
 ↓
Frame
 ↓
Packet
 ↓
Segment
 ↓
Data
</pre>

<p>
<strong>Encapsulation = Adding information</strong>
</p>

<p>
<strong>Decapsulation = Removing information</strong>
</p>

<hr>

<h2>5. Data Units</h2>

<p>
As data moves through the network layers, it has different names.
</p>

<pre>
Application  → Data
Transport    → Segment
Network      → Packet
Data Link    → Frame
Physical     → Bits
</pre>

<p>For example, when your browser sends information:</p>

<pre>
Data → Segment → Packet → Frame → Bits
</pre>

<p>When the server receives it:</p>

<pre>
Bits → Frame → Packet → Segment → Data
</pre>

<p>
These terms are important because they are commonly used in networking and SOC investigations.
</p>

<hr>

<h2>6. Network Devices &amp; Layers</h2>

<table>
  <thead>
    <tr>
      <th>Device</th>
      <th>Common Layer</th>
      <th>Purpose</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Hub</strong></td>
      <td>Layer 1</td>
      <td>Sends traffic to all ports</td>
    </tr>
    <tr>
      <td><strong>Switch</strong></td>
      <td>Layer 2</td>
      <td>Connects devices in a LAN</td>
    </tr>
    <tr>
      <td><strong>Router</strong></td>
      <td>Layer 3</td>
      <td>Connects different networks</td>
    </tr>
    <tr>
      <td><strong>Firewall</strong></td>
      <td>Layer 3–7</td>
      <td>Controls network traffic</td>
    </tr>
    <tr>
      <td><strong>Access Point</strong></td>
      <td>Layer 2</td>
      <td>Provides wireless connectivity</td>
    </tr>
  </tbody>
</table>

<p><strong>Example:</strong></p>

<pre>
Laptop
   ↓
Switch       → Local Network
   ↓
Router       → Other Networks
   ↓
Firewall     → Traffic Control
   ↓
Internet
</pre>

<p>
<strong>SOC Perspective:</strong> Knowing the network layer helps you understand what type of traffic or attack you are investigating.
</p>

<hr>

<h2>7. End-to-End Communication</h2>

<p>
<strong>End-to-end communication</strong> means understanding the complete journey of data between two endpoints.
</p>

<p><strong>Example: Opening a Website</strong></p>

<pre>
Your Laptop
     ↓
Wi-Fi / Switch
     ↓
Router
     ↓
Firewall
     ↓
Internet
     ↓
Web Server
</pre>

<p>
The server then sends the response back:
</p>

<pre>
Web Server
     ↓
Internet
     ↓
Firewall
     ↓
Router
     ↓
Switch / Wi-Fi
     ↓
Your Laptop
</pre>

<p>
<strong>SOC L1 Perspective:</strong> When investigating a network alert, you want to understand:
</p>

<pre>
Source
   ↓
Destination
   ↓
Protocol
   ↓
Port
   ↓
Network Path
   ↓
What Happened
</pre>
