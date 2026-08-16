<h1>Chapter 13 — Wireless &amp; Remote Networking</h1>
<img width="800" height="1200" alt="image" src="https://github.com/user-attachments/assets/c31eea0f-ad1a-42f3-81ad-3aaefed50b59" />
<p>
Wireless networking allows devices to communicate without physical
network cables, while remote networking allows users or networks to
connect from different locations.
</p>

<hr>

<h2>13.1 Wi-Fi Basics</h2>

<p>
<strong>Wi-Fi</strong> is a wireless networking technology that allows
devices to communicate using radio signals instead of physical Ethernet
cables.
</p>

<p>Examples of wireless devices:</p>

<ul>
  <li>Laptop</li>
  <li>Smartphone</li>
  <li>Tablet</li>
  <li>Smart Devices</li>
</ul>

<p>
A Wi-Fi network normally uses an <strong>Access Point (AP)</strong> to
provide wireless connectivity.
</p>

<p>
<strong>Simple meaning:</strong><br>
Wi-Fi = Network communication without a physical network cable.
</p>

<hr>

<h2>13.2 SSID</h2>

<p>
<strong>SSID = Service Set Identifier</strong>
</p>

<p>
SSID is the <strong>name of a Wi-Fi network</strong> that users see when
searching for available wireless networks.
</p>

<h3>Example</h3>

<pre>
Available Wi-Fi:

Home_WiFi
Office_WiFi
Guest_WiFi
</pre>

<p>
Here, <code>Office_WiFi</code> is the SSID.
</p>

<p>
<strong>SSID = Wi-Fi network name</strong>
</p>

<hr>

<h2>13.3 Access Point</h2>

<p>
An <strong>Access Point (AP)</strong> is a device that provides wireless
network connectivity to clients.
</p>

<p>
It allows wireless devices to connect to the network.
</p>

<pre>
Laptop  ))))
          ↓
     Access Point
          ↓
       Network
</pre>

<p>
In an enterprise environment, multiple access points may be deployed
across different areas.
</p>

<hr>

<h2>13.4 Wireless Clients</h2>

<p>
A <strong>wireless client</strong> is a device that connects to a
Wi-Fi network.
</p>

<p>Examples:</p>

<ul>
  <li>Laptop</li>
  <li>Mobile Phone</li>
  <li>Tablet</li>
  <li>Wireless Printer</li>
  <li>IoT Device</li>
</ul>

<pre>
Wireless Client
      ↓
Access Point
</pre>

<p>
The client needs to associate with the Access Point before communicating
through the wireless network.
</p>

<hr>

<h2>13.5 2.4 GHz &amp; 5 GHz</h2>

<p>
Wi-Fi commonly operates on different radio frequency bands.
</p>

<h3>2.4 GHz</h3>

<ul>
  <li>Longer range</li>
  <li>Better penetration through walls</li>
  <li>More likely to experience interference</li>
  <li>Usually lower speeds than 5 GHz</li>
</ul>

<h3>5 GHz</h3>

<ul>
  <li>Higher potential speeds</li>
  <li>More available channels</li>
  <li>Shorter range compared with 2.4 GHz</li>
  <li>Generally less congestion</li>
</ul>

<p>
<strong>2.4 GHz → Better range</strong><br>
<strong>5 GHz → Better speed / generally less interference</strong>
</p>

<p>
Actual performance depends on the environment, channel, Wi-Fi standard,
and device.
</p>

<hr>

<h2>13.6 WPA2 &amp; WPA3</h2>

<p>
<strong>WPA = Wi-Fi Protected Access</strong>
</p>

<p>
WPA2 and WPA3 are security standards used to protect Wi-Fi networks.
</p>

<p>They help provide:</p>

<ul>
  <li>Authentication</li>
  <li>Encryption</li>
  <li>Protection of wireless communication</li>
</ul>

<h3>WPA2</h3>

<p>
WPA2 is widely deployed and commonly uses AES-based encryption.
</p>

<h3>WPA3</h3>

<p>
WPA3 is a newer Wi-Fi security standard that provides stronger
security features.
</p>

<p>
<strong>WPA2 → Common and secure</strong><br>
<strong>WPA3 → Newer and stronger security</strong>
</p>

<hr>

<h2>13.7 Wireless Authentication</h2>

<p>
Before a device gets access to a protected Wi-Fi network, it usually
needs to <strong>authenticate</strong>.
</p>

<p>
For a simple home network, this may involve a Wi-Fi password.
</p>

<p>
In an enterprise environment, authentication can involve:</p>

<ul>
  <li>User Credentials</li>
  <li>RADIUS</li>
  <li>802.1X</li>
</ul>

<pre>
Client
  ↓
Authentication
  ↓
Access Point
  ↓
Network Access
</pre>

<p>
<strong>
Wireless authentication = Verifying that a device or user is allowed
to connect.
</strong>
</p>

<hr>

<h2>13.8 VPN</h2>

<p>
<strong>VPN = Virtual Private Network</strong>
</p>

<p>
A VPN creates a protected connection over an untrusted network such as
the Internet.
</p>

<pre>
User → Internet → VPN → Company Network
</pre>

<p>
VPN can be used for both <strong>remote access</strong> and
<strong>site-to-site connectivity</strong>.
</p>

<hr>

<h2>13.9 Remote Access</h2>

<p>
<strong>Remote access</strong> means accessing a network or system from
a different location.
</p>

<p>Example:</p>

<pre>
Employee Working From Home
          ↓
    Company Network
</pre>

<p>
A VPN is commonly used to provide secure remote access.
</p>

<p>
The user normally authenticates before being given access to permitted
resources.
</p>

<hr>

<h2>13.10 Site-to-Site VPN</h2>

<p>
A <strong>Site-to-Site VPN</strong> connects two networks through a
protected VPN connection.
</p>

<pre>
Head Office
     │
 VPN Tunnel
     │
Branch Office
</pre>

<p>
The VPN connection is normally established between VPN gateways.
</p>

<p>
<strong>
Site-to-Site VPN = Network-to-Network connection
</strong>
</p>

<hr>

<h2>13.11 Remote-Access VPN</h2>

<p>
A <strong>Remote-Access VPN</strong> connects an individual user or
device to an organization's network.
</p>

<pre>
Employee Laptop
       ↓
    Internet
       ↓
  VPN Gateway
       ↓
Company Network
</pre>

<h3>Remote Access vs Site-to-Site</h3>

<table>
  <thead>
    <tr>
      <th>Remote-Access VPN</th>
      <th>Site-to-Site VPN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>User → Network</td>
      <td>Network → Network</td>
    </tr>
    <tr>
      <td>Individual device connects</td>
      <td>Entire network connects</td>
    </tr>
    <tr>
      <td>Commonly used by remote employees</td>
      <td>Commonly used by offices / branches</td>
    </tr>
    <tr>
      <td>Laptop can be the endpoint</td>
      <td>VPN gateways are typically the endpoints</td>
    </tr>
  </tbody>
</table>
<hr>
<h2>🎯 SOC L1 Perspective</h2>

<p>
Wireless and VPN information can be useful during security
investigations.
</p>

<p>An analyst may investigate:</p>

<ul>
  <li>Wireless authentication failures</li>
  <li>Unknown devices</li>
  <li>Repeated Wi-Fi authentication attempts</li>
  <li>VPN login failures</li>
  <li>Successful VPN connections</li>
  <li>Source IP</li>
  <li>User or account</li>
  <li>Connection time</li>
  <li>VPN-assigned IP</li>
</ul>

<p>
The main questions for a SOC analyst are:
</p>

<pre>
Who connected?
From where?
When?
Was authentication successful?
What network access was provided?
</pre>

<p>
Understanding these details helps an analyst identify unusual wireless
or remote-access activity.
</p>
```

