<h1>Chapter 15 — Network Troubleshooting</h1>
<img width="800" height="1200" alt="image" src="https://github.com/user-attachments/assets/56b27458-d89b-4c3e-9ff9-38a9c2ca0cbe" />

<p>
Network troubleshooting is the process of identifying and fixing problems
that prevent systems from communicating correctly over a network.
</p>

<hr>

<h2>15.1 Ping</h2>

<p>
<strong>Ping</strong> is used to check whether a destination is reachable
over the network and to measure the response time.
</p>

<p>
It commonly uses <strong>ICMP Echo Request and Echo Reply</strong>.
</p>

<pre>
ping 8.8.8.8
</pre>

<p>You can check:</p>

<ul>
  <li>Is the destination reachable?</li>
  <li>How long does it take to respond?</li>
  <li>Are packets being lost?</li>
</ul>

<p>
<strong>Simple meaning:</strong><br>
Ping = Basic reachability test.
</p>

<hr>

<h2>15.2 Traceroute / Tracert</h2>

<p>
<strong>Traceroute</strong> shows the network hops between your system
and a destination.
</p>

<p><strong>Windows:</strong></p>

<pre>
tracert 8.8.8.8
</pre>

<p><strong>Linux:</strong></p>

<pre>
traceroute 8.8.8.8
</pre>

<p>
It can help identify where communication may be slowing down or failing.
</p>

<p>
<strong>Simple meaning:</strong><br>
Traceroute = Shows the path/hops toward a destination.
</p>

<hr>

<h2>15.3 IP Configuration</h2>

<p>
IP configuration commands help you see the network settings of a device.
</p>

<p><strong>Windows:</strong></p>

<pre>
ipconfig
</pre>

<p><strong>Linux:</strong></p>

<pre>
ip addr
</pre>

<p>You can check information such as:</p>

<ul>
  <li>IP Address</li>
  <li>Subnet Mask / Prefix</li>
  <li>Default Gateway</li>
  <li>Network Interface Status</li>
</ul>

<p>
This is useful when a system cannot communicate with other networks.
</p>

<hr>

<h2>15.4 ARP Commands</h2>

<p>
<strong>ARP (Address Resolution Protocol)</strong> helps map an IPv4
address to a MAC address on the local network.
</p>

<pre>
IP Address → MAC Address
</pre>

<p>
You can inspect the ARP cache to see recently learned mappings.
</p>

<p><strong>Windows:</strong></p>

<pre>
arp -a
</pre>

<p><strong>Linux:</strong></p>

<pre>
ip neigh
</pre>

<p>
Unexpected or changing IP-to-MAC mappings can sometimes be worth
investigating.
</p>

<hr>

<h2>15.5 DNS Lookup</h2>

<p>
DNS lookup helps check whether a domain name can be resolved to an
IP address.
</p>

<pre>
nslookup google.com
</pre>

<p>or:</p>

<pre>
dig google.com
</pre>

<p>You can check:</p>

<ul>
  <li>Domain Name</li>
  <li>Returned IP Address</li>
  <li>DNS Server being used</li>
  <li>Whether resolution is successful</li>
</ul>

<p>
<strong>Simple meaning:</strong><br>
DNS lookup = Check whether a domain name resolves correctly.
</p>

<hr>

<h2>15.6 Netstat / SS</h2>

<p>
These commands show information about network connections and
listening ports.
</p>

<p><strong>Windows:</strong></p>

<pre>
netstat -ano
</pre>

<p><strong>Linux:</strong></p>

<pre>
ss -tulnp
</pre>

<p>You can identify:</p>

<ul>
  <li>Listening Ports</li>
  <li>Active Connections</li>
  <li>Source and Destination Addresses</li>
  <li>Connection States</li>
  <li>Associated Processes (depending on command and permissions)</li>
</ul>

<p>
For a SOC analyst, this can help identify unexpected network
connections or services.
</p>

<hr>

<h2>15.7 Routing Information</h2>

<p>
Routing information tells you how a system decides where to send
IP traffic.
</p>

<p>
You can inspect the routing table.
</p>

<p><strong>Windows:</strong></p>

<pre>
route print
</pre>

<p><strong>Linux:</strong></p>

<pre>
ip route
</pre>

<p>Important information includes:</p>

<ul>
  <li>Destination Network</li>
  <li>Next Hop</li>
  <li>Interface</li>
  <li>Default Route</li>
</ul>

<p>
A wrong or missing route can cause connectivity problems.
</p>

<hr>

<h2>15.8 Port Connectivity</h2>

<p>
Sometimes the host is reachable, but a <strong>specific service or
port</strong> is not accessible.
</p>

<pre>
Server IP → 10.10.1.20
Port      → 443
</pre>

<p>
You can test whether the service is reachable using:
</p>

<pre>
Test-NetConnection 10.10.1.20 -Port 443
</pre>

<p>
Tools such as <code>nc</code> or <code>telnet</code> may also be used
where appropriate.
</p>

<p>
<strong>Important:</strong>
</p>

<blockquote>
  Ping working does NOT mean every port is accessible.
</blockquote>

<hr>

<h2>15.9 Connectivity Problems</h2>

<p>
Network connectivity can fail for many reasons.
</p>

<p>Common examples:</p>

<ul>
  <li>Incorrect IP Configuration</li>
  <li>DNS Failure</li>
  <li>Wrong Gateway</li>
  <li>Routing Problem</li>
  <li>Firewall Blocking Traffic</li>
  <li>Service Not Running</li>
  <li>Port Blocked</li>
  <li>Network Interface Problem</li>
  <li>Physical / Wi-Fi Connectivity Issue</li>
</ul>

<p>
The key is to identify <strong>where the communication is failing</strong>
instead of randomly changing settings.
</p>

<hr>

<h2>15.10 Basic Troubleshooting</h2>

<p>
Basic troubleshooting means checking network communication
systematically.
</p>

<p>Useful checks include:</p>

<ul>
  <li>IP Configuration</li>
  <li>Local Connectivity</li>
  <li>Default Gateway</li>
  <li>DNS Resolution</li>
  <li>Routing</li>
  <li>Port Connectivity</li>
  <li>Firewall Rules</li>
  <li>Service Availability</li>
</ul>

<p>
The goal is to determine whether the problem is with the
<strong>device, network, DNS, route, firewall, port, or
application/service</strong>.
</p>

<hr>
<h2>🎯 SOC L1 Perspective</h2>

<p>
These commands are useful for validating alerts and understanding
network behavior.
</p>

<p>A SOC analyst may need to determine:</p>

<pre>
Which IP?
   ↓
Which Route?
   ↓
Which Port?
   ↓
Which Service?
   ↓
Is the Connection Expected?
</pre>

<p>
This helps distinguish a <strong>normal connectivity issue</strong>
from potentially suspicious network activity.
</p>
