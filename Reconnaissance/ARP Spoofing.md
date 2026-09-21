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
