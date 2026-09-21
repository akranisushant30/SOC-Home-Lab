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
<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/d994b4db-92b0-4cb9-9127-95f2d371c4b9" />
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
