<h2>🔎 Investigation Phase</h2>
<p>I received a High-severity alert on `EliotPRD` because the requested URL contained the string `ls`. Since the request was allowed, I need to check whether it was a normal search request or something suspicious.</p>
<h3>🚨 Step 1 — Alert Triage &amp; Scope</h3>
<h4>SOC L1 Thinking</h4>
<blockquote><p>I will start by reviewing the alert rule and examining the traffic details to understand what triggered the detection and which devices were involved.</p></blockquote>
<h4>1. Alert Review</h4>
<img width="1358" height="585" alt="image" src="https://github.com/user-attachments/assets/0b4629e1-19e9-446d-a047-5fe6d5e80318" />
<p>Here, the alert was triggered because the URL contains the string <code>ls</code>. The GET request was allowed and was associated with the host <code>EliotPRD</code>.</p>
<h4>2. Collect Data</h4>
<blockquote>
<p>First, I'll gather information about the source IP's & Destination IP's ownership and reputation.</p>
</blockquote>
<h6>Source IP Ownership Check - Whois 172.16.17.46</h6>
<img width="802" height="456" alt="image" src="https://github.com/user-attachments/assets/d4af17f3-41c1-46f1-8a90-55a67249c1dd" />
<p>First, I checked the IP address in our internal network and found that it was assigned to the device <code>EliotPRD</code>, which was used by the user <code>eliot</code>. The last recorded login was on <code>2022-02-27 02:30:01</code>. Since this is a private IP address, there was no need to check its public IP reputation.</p>
<h6>Destination IP Ownership Check - Whois 188.114.96.15</h6>
<img width="794" height="824" alt="image" src="https://github.com/user-attachments/assets/8f7f596e-8797-48a8-98e0-9ddde6ee0a20" />
<p>I checked the WHOIS details and found that it belongs to Cloudflare, Inc. The IP range is registered under <code>CLOUDFLARENET-EU</code> and is associated with AS13335.</p>
<h6>Destination Reputation Check - Whois 188.114.96.15</h6>
<img width="562" height="591" alt="image" src="https://github.com/user-attachments/assets/e5472dbc-2434-4d1d-8870-399691f77a8e" />
<p>I checked the IP address on AbuseIPDB and found an abuse confidence score of <code>0%</code>. The IP belongs to Cloudflare's reverse proxy network and has 7 historical reports.</p>
<h3>📋 Step 2 — Relevant Log Analysis</h3>
<h4>🧠 SOC L1 Thinking</h4>
<blockquote>
<p>I will review the request details and related web logs to understand why the alert was triggered and whether the request contains any suspicious activity.</p></blockquote>
<h5>1. HTTP Traffic Analysis</h5>
<img width="1752" height="687" alt="image" src="https://github.com/user-attachments/assets/debe7445-674f-4319-a812-14ec2d8eefbb" />
<p>The HTTP logs showed multiple GET requests to LetsDefend blog pages. All requests were permitted and returned HTTP status <code>200</code>. The alert was triggered by the URL <code>https://letsdefend.io/blog/?s=skills</code>, where <code>skills</code> appears to be a normal search query rather than an obvious command payload.</p>
<h3>🔗 Step 3 — Evidence Correlation &amp; Impact Check</h3>
<h4>🧠 SOC L1 Thinking</h4>
<blockquote>
<p>The HTTP logs showed permitted requests to LetsDefend blog pages with successful responses. I will use these findings to assess whether the traffic was malicious and check for any other suspicious activity.</p></blockquote>
<ul>
  <li><strong>Traffic:</strong> Non-Malicious</li>
  <li><strong>Other Suspicious Traffic:</strong> Not Found</li>
</ul>
<h4>🖥️ Endpoint History Analysis</h4>
<p>I reviewed the endpoint history to check whether the device showed any other suspicious activity related to the alert. No suspicious activity was found.</p>
<img width="1540" height="624" alt="image" src="https://github.com/user-attachments/assets/78e4a0e0-6dab-408d-bcce-4f62745425da" />
<h3>⚖️ Step 4 — Final Assessment</h3>

<h4>🧠 SOC L1 Thinking</h4>
<blockquote>
<p>Based on the investigation, I will confirm the final alert classification using the evidence collected.</p></blockquote>

<h4>📋 Alert Classification</h4>

<ul>
  <li><strong>Final Verdict:</strong> False Positive</li>
  <li><strong>Reason:</strong> The alert was triggered by a normal search query, and no malicious activity was identified during the investigation.</li>
</ul>

<h3>✅ Step 5 — Alert Closure</h3>

<p>The alert was closed as a False Positive after the investigation found no evidence of malicious activity.</p>
