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

<h4>Step 1 Findings</h4>

<p>The source IP belongs to DigitalOcean, LLC, and multiple VirusTotal vendors flagged it as suspicious or phishing-related. The requested URL contains a SQL injection-like payload, and the device action was recorded as Allowed. At this stage, the request is suspicious, but successful exploitation has not been confirmed.</p>
<h3>Step 2: Relevant Log Analysis</h3>

<p><strong>SOC L1 Thinking:</strong> Since the source IP has been flagged as suspicious and the URL contains a SQL injection-like payload, I'll examine the HTTP request to understand what was sent to the web server.</p>
<h4>1. Examine HTTP Traffic</h4>
<p> Multiple firewall events show connections from <code>167.99.169.17</code> to <code>172.16.17.18:443</code> at different timestamps.</p>
<img width="1761" height="655" alt="image" src="https://github.com/user-attachments/assets/77cca2a0-b377-45c9-a421-7136718393a1" />
<p>I reviewed the raw HTTP logs and decoded the requested URLs to understand the inputs sent to the web server. During this review, I found multiple requests containing SQL injection-like payloads targeting the search endpoint.</p>
<img width="1913" height="657" alt="image" src="https://github.com/user-attachments/assets/7c47d123-c0b3-4235-8496-d42c5183dfcb" />
<p>The decoded URLs included single-quote tests, <code>OR</code> conditions, and an <code>ORDER BY</code> clause, indicating repeated SQL injection testing attempts.</p>

<h4>Findings</h4>
<p>After reviewing the raw HTTP logs and decoding the requested URLs, I found multiple requests containing SQL injection-like payloads targeting the search endpoint. The requests included single quotes, <code>OR</code> conditions, and an <code>ORDER BY</code> clause. All five search requests returned HTTP 500 errors with the same response size of 948 bytes. Further investigation is needed to determine whether the attack was successful.</p>
<h3>Step 3: Correlation &amp; Impact</h3>
<p><strong>SOC L1 Thinking:</strong> Since multiple SQL injection-like requests were found in the HTTP logs, I'll correlate the available events and check whether the traffic was part of a planned test. I'll also investigate whether there is any evidence that the attack was successful.</p>

<h4>Attack Type</h4>

<p>Based on the decoded URLs, I identified the attack type as SQL Injection (SQLi).</p>

<h4>Planned Test Check</h4>

<p>I checked the mailbox for any emails about planned security testing but couldn't find any. The available alert details also didn't indicate that the traffic came from an attack simulation tool.</p>

<h4>Traffic Direction</h4>

<p>I identified the traffic direction as Internet to Company because the external source IP <code>167.99.169.17</code> was targeting the internal web server <code>172.16.17.18</code>.</p>

<h4>Attack Success Check</h4>

<p>I checked the Command History for any suspicious commands but didn't find anything related to the attack. I also reviewed the HTTP responses, and all five search requests returned a 500 error with the same response size.</p>

<p>Based on what I found, I couldn't confirm that the SQL injection attempt was successful.</p>

<h4>Step 3 Findings</h4>

<p>I found multiple SQL injection attempts from an external IP, with no evidence of a planned test. I also checked Command History but found no suspicious commands. The available logs did not confirm whether the attack was successful.</p>

<h3>Step 4: Assessment</h3>

<blockquote><p>Based on the investigation, I classified the alert as a <strong>True Positive</strong> with <strong>High</strong> severity. Multiple SQL injection attempts were found in the HTTP logs, but no evidence confirmed successful exploitation.</p></blockquote>

<p><strong>MITRE ATT&amp;CK:</strong> T1190 – Exploit Public-Facing Application</p>
<img width="1040" height="379" alt="image" src="https://github.com/user-attachments/assets/2229e12f-b090-4c68-8507-d2174310de2c" />


<h3>Step 5: Action</h3>

<p>No Tier 2 escalation was required because the attack was from the Internet and no evidence of successful exploitation was found.</p>
