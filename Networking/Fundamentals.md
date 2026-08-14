<h1>Chapter 1 — Network Fundamentals</h1>

<h2>Topic 1.1 — Network Fundamentals</h2>

<h3>What is a Network?</h3>

<p>
A network is an interconnected system of devices that allows them
to communicate and exchange data with each other.
</p>

<p>
A network is not simply a group of computers connected together.
For communication to work properly, devices need connectivity,
addressing, communication protocols, and network services.
</p>

<p>
The main building blocks of a network include endpoints, network
devices, network interfaces, addressing, protocols, and services.
</p>

<table>
<tr>
<td align="center" bgcolor="#E8F1FF">
💻<br>
<strong>Laptop</strong><br>
<sub>Endpoint</sub>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#EAF7EE">
🔀<br>
<strong>Switch</strong><br>
<sub>Local Network</sub>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#FFF4E5">
🌐<br>
<strong>Router</strong><br>
<sub>Network Routing</sub>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#F1ECFF">
🌍<br>
<strong>Internet</strong>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#EAF7EE">
🖥️<br>
<strong>Web Server</strong><br>
<sub>Endpoint</sub>
</td>
</tr>
</table>

<p>
In this example, the laptop and web server are endpoints.
The switch provides connectivity within the local network,
while the router provides communication between different networks.
</p>

<h3>Endpoints and Network Devices</h3>

<p>
An endpoint is a device that sends or receives data on a network.
Common examples include laptops, desktop computers, servers,
printers, and other connected devices.
</p>

<p>
Network devices are responsible for connecting devices and
forwarding or controlling network traffic.
</p>

<ul>
    <li><strong>Switch:</strong> Connects devices within a local network.</li>
    <li><strong>Router:</strong> Connects different networks and forwards traffic between them.</li>
    <li><strong>Firewall:</strong> Controls network traffic according to configured rules.</li>
    <li><strong>Wireless Access Point:</strong> Provides wireless connectivity to network devices.</li>
</ul>

<p>
Each device has a different role, but they work together to provide
end-to-end communication.
</p>

<h3>How Networks Work in the Real World</h3>

<p>
In a real organization, devices are usually not connected through
one simple network. Networks are commonly divided into different
sections based on the purpose of the devices and the type of
communication required.
</p>

<table>
<tr>
<td align="center" bgcolor="#F1ECFF">
🌍<br>
<strong>Internet</strong>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#FFECEC">
🛡️<br>
<strong>Firewall</strong>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#FFF4E5">
🌐<br>
<strong>Router</strong>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#E8F1FF">
🏢<br>
<strong>Core Network</strong>
</td>
</tr>
</table>

<table>
<tr>
<td align="center" bgcolor="#EAF7EE">
👥<br>
<strong>User Network</strong>
</td>

<td align="center">↔️</td>

<td align="center" bgcolor="#F1ECFF">
🖥️<br>
<strong>Server Network</strong>
</td>

<td align="center">↔️</td>

<td align="center" bgcolor="#FFF4E5">
⚙️<br>
<strong>Management Network</strong>
</td>
</tr>
</table>

<p>
An organization may have separate networks for employee devices,
servers, network management, guest devices, and systems that need
to communicate with the Internet.
</p>

<p>
This separation allows organizations to control how different parts
of the network communicate with each other.
</p>

<h3>Network Communication</h3>

<p>
When one device communicates with another device, multiple networking
technologies work together to move the data from the source to the
destination.
</p>

<p>
For example, imagine a laptop communicating with a server located
on another network.
</p>

<ul>
    <li>Laptop: <code>192.168.10.20</code></li>
    <li>Server: <code>192.168.20.50</code></li>
</ul>

<p>
The laptop first creates data through an application. The operating
system then uses the networking stack to prepare that data for
transmission.
</p>

<p>
The laptop needs to determine where the destination is. In an IPv4
network, it checks whether the destination belongs to the same local
network or to another network.
</p>

<h3>Same Network vs Different Network</h3>

<p>
If the destination is on the same local network, the source device
can communicate with the destination through the local network.
</p>

<table>
<tr>
<td align="center" bgcolor="#E8F1FF">
💻<br>
<strong>Source Device</strong>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#EAF7EE">
🔀<br>
<strong>Local Network</strong>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#EAF7EE">
🖥️<br>
<strong>Destination</strong>
</td>
</tr>
</table>

<p>
If the destination is on another network, the traffic normally needs
to be sent to the default gateway.
</p>

<p>
The default gateway is usually a router or Layer 3 device that
provides a path from the local network to other networks.
</p>

<table>
<tr>
<td align="center" bgcolor="#E8F1FF">
💻<br>
<strong>Source Device</strong>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#FFF4E5">
🌐<br>
<strong>Default Gateway</strong>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#F1ECFF">
🌍<br>
<strong>Other Network</strong>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#EAF7EE">
🖥️<br>
<strong>Destination</strong>
</td>
</tr>
</table>

<p>
In an IPv4 Ethernet network, ARP may be used to determine the MAC
address associated with a local IPv4 address. This allows the device
to create the Ethernet frame needed for local delivery.
</p>

<h3>How Traffic Moves Between Networks</h3>

<p>
When traffic reaches a router, the router examines the destination
IP address and uses its routing information to determine where the
packet should be forwarded next.
</p>

<p>
The traffic can pass through multiple networks and routing devices
before reaching the destination network.
</p>

<table>
<tr>
<td align="center" bgcolor="#E8F1FF">
💻<br>
<strong>Source Device</strong>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#EAF7EE">
🔀<br>
<strong>Local Network</strong>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#FFF4E5">
🌐<br>
<strong>Router</strong>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#F1ECFF">
🌍<br>
<strong>Another Network</strong>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#FFF4E5">
🌐<br>
<strong>Router / Switch</strong>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#EAF7EE">
🖥️<br>
<strong>Destination Device</strong>
</td>
</tr>
</table>

<p>
Once the traffic reaches the destination network, it is delivered
to the destination device. The destination device then passes the
data to the appropriate network service or application.
</p>

<h3>Example: Employee Accessing an Internal Application</h3>

<p>
Consider an employee using a laptop to access an internal company
application.
</p>

<table>
<tr>
<td align="center" bgcolor="#E8F1FF">
💻<br>
<strong>Employee Laptop</strong>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#EAF7EE">
🔀<br>
<strong>Access Switch</strong>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#FFF4E5">
🌐<br>
<strong>Router / Layer 3 Device</strong>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#FFECEC">
🛡️<br>
<strong>Firewall</strong>
</td>

<td align="center">➡️</td>

<td align="center" bgcolor="#F1ECFF">
🖥️<br>
<strong>Application Server</strong>
</td>
</tr>
</table>

<p>
The laptop sends traffic into the local network. The switch provides
local connectivity. If the destination is on another network, the
traffic is forwarded toward a routing device.
</p>

<p>
Depending on the organization's architecture, the traffic may pass
through a firewall before reaching the application server.
</p>

<p>
The important point is that every network component has a specific
role in moving or controlling the traffic.
</p>
he detailed concepts behind ARP, Ethernet, IP addressing, routing,
TCP, UDP, DNS, and other protocols will be covered in later chapters.
</p>
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/a9e7264c-1457-4031-a3a5-4ad3a6f5a61a" />

