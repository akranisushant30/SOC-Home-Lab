<h2>🔎 Investigation Overview</h2>

<p>A High-severity alert was raised for a possible SQL injection attempt targeting <code>WebServer1001</code>. The request came from <code>167.99.169.17</code>, and the device action was recorded as <strong>Allowed</strong>.</p>
<h3>🚨 Step 1 — Alert Triage & Scope</h3>

<h6>SOC L1 Thinking</h6>

<blockquote>
Before checking the logs, I'll first understand what triggered this alert and where the request came from.
</blockquote>
<h4>1. Alert Review</h4>

<img width="1545" height="518" alt="image" src="https://github.com/user-attachments/assets/d447fb1a-d624-4149-ae70-300745620ede" />
<p>The alert was triggered because the requested URL contained a possible SQL injection payload. The request came from <code>167.99.169.17</code> and was directed to the internal web server <code>172.16.17.18</code> (<code>WebServer1001</code>).</p>

<p>The request used HTTPS with the GET method, and the device action was recorded as <strong>Allowed</strong>. This means the request was allowed, but it doesn't confirm whether the SQL injection was successful.</p>
<h4>URL Decoding</h4>

<p>The requested URL contains encoded characters, so I'll decode it to understand what payload was sent in the request.</p>
<img width="1363" height="628" alt="image" src="https://github.com/user-attachments/assets/af4237d0-85d0-4b90-b965-ca169b6e7454" />
<p>The decoded payload contains a common SQL injection pattern, which helps explain why the alert was triggered.</p>
<h4>2. Collect Data</h4>

<blockquote>
I'll check the source IP's ownership and reputation, along with the available details of the target server.
</blockquote>
<h6>Source IP Ownership Check - Whois IP 167.99.169.17</h6>
<img width="908" height="631" alt="image" src="https://github.com/user-attachments/assets/827a8cd2-9c65-4be9-ab89-84ddc8decbdd" />
<table>
  <thead>
    <tr>
      <th>Field</th>
      <th>Observed Data</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>NetRange</td><td><code>167.99.0.0 - 167.99.255.255</code></td></tr>
    <tr><td>CIDR</td><td><code>167.99.0.0/16</code></td></tr>
    <tr><td>NetName</td><td><code>DIGITALOCEAN-167-99-0-0</code></td></tr>
    <tr><td>Organization</td><td>DigitalOcean, LLC</td></tr>
    <tr><td>Org ID</td><td><code>DO-13</code></td></tr>
    <tr><td>Country</td><td>United States (US)</td></tr>
    <tr><td>Net Type</td><td>Direct Allocation</td></tr>
    <tr><td>Registration Date</td><td>2017-11-10</td></tr>
    <tr><td>Abuse Contact</td><td>DigitalOcean Abuse</td></tr>
    <tr>
      <td>WHOIS Source</td>
      <td><a href="https://rdap.arin.net/registry/ip/167.99.169.17">ARIN RDAP Lookup</a></td>
    </tr>
  </tbody>
</table>
<h6>Source IP Reputation Check</h6>
<p> I'll check whether security vendors have flagged the source IP for suspicious activity.</p>
<img width="1342" height="562" alt="image" src="https://github.com/user-attachments/assets/fa5e60a1-1f4c-4073-8a08-f6012b28af29" />
