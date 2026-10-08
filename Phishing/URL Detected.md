<h2>🔎 Investigation Phase</h2>

<img width="1588" height="468" alt="image" src="https://github.com/user-attachments/assets/bdbc13c3-01dd-4fcb-ab7f-7c1597ed176c" />

<p>The alert was generated for a <strong>High-severity phishing URL detection</strong> involving user <strong>ellie</strong> on <strong>EmilyComp (172.16.17.49)</strong>. The user accessed a suspicious URL on <strong>mogagrocol.ru (91.189.114.8)</strong>, and the request was <strong>allowed</strong> by the device.</p>

<p>Since the request was allowed, the investigation focuses on understanding what the user accessed, whether the destination and URL are associated with phishing activity, and whether there is any evidence of further impact on the user or system.</p>
<h3>🚨 Step 1 — Alert Triage & Scope</h3>

<h6>SOC L1 Thinking</h6>

<blockquote>
The alert has identified a suspicious phishing URL, but I first need to understand the basic details of the connection. I will collect the source address, destination address, and user-agent to identify where the request came from, where it was going, and what client was used to access it.
</blockquote>
<h4>1. Source & Destination Address</h4>

<pre><code>Source Address equals "172.16.17.49" AND Destination Address equals "91.189.114.8"</code></pre>
<img width="1538" height="516" alt="image" src="https://github.com/user-attachments/assets/9ca21b85-127e-4060-8a29-06469576ec2f" />
<p>The search returned two events for the same source and destination:</p>

<ul>
  <li><strong>Firewall:</strong> 172.16.17.49:55662 → 91.189.114.8:80 at 2021-03-22 23:53:16</li>
  <li><strong>Proxy:</strong> 172.16.17.49:55662 → 91.189.114.8:80 at 2021-03-22 23:53:54</li>
</ul>

<p>The Proxy event recorded the following request URL:</p>

<pre><code>http://mogagrocol.ru/wp-content/plugins/akismet/fv/index.php?email=ellie@letsdefend.io</code></pre>

<blockquote>
<strong>Finding:</strong> The activity originated from <strong>172.16.17.49</strong> and connected to <strong>91.189.114.8</strong> over HTTP port <strong>80</strong>. Both Firewall and Proxy events confirm the same communication, while the Proxy event recorded the suspicious URL accessed by the user.
</blockquote>
<h4>2. User-Agent</h4>

<p>The alert details also provided the following User-Agent:</p>

<pre><code>Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.88 Safari/537.36</code></pre>

<blockquote>
<strong>Finding:</strong> The User-Agent indicates that the request originated from a 64-bit Windows system using Chrome 79.0.3945.88. This provides context about the client used to access the URL, but does not by itself confirm malicious activity.
</blockquote>

<blockquote>
<strong>Step 1 Finding:</strong> The alert involved a request from <strong>172.16.17.49</strong> to <strong>91.189.114.8</strong> over HTTP port <strong>80</strong>. The communication was observed in both Firewall and Proxy events, and the Proxy event identified the requested URL on <strong>mogagrocol.ru</strong>. The alert also provided a Windows-based Chrome User-Agent for the request. The request was allowed by the device.
</blockquote>

<h3>🔎 Step 2 — Relevant Log Analysis</h3>

<h6>SOC L1 Thinking</h6>

<blockquote>
Now that I have identified the suspicious URL, I need to check its reputation and see whether it has been flagged for phishing or other malicious activity.
</blockquote>
<h4>1. URL Reputation Check</h4>
<img width="1881" height="806" alt="image" src="https://github.com/user-attachments/assets/9ddd09a8-3bc7-4cbe-a4ff-9d7bddca0ae4" />
<blockquote>
<strong>Finding:</strong> Multiple security vendors flagged the URL as <strong>Phishing</strong>, while other vendors classified it as <strong>Malicious</strong>, <strong>Malware</strong>, or <strong>Suspicious</strong>. This indicates that the URL has a malicious/phishing reputation.
</blockquote>
<h4>2. URL Details Analysis</h4>
<p>VirusTotal's Details section was reviewed to understand the URL's history, destination, and observed HTTP activity.</p>
<img width="1842" height="860" alt="image" src="https://github.com/user-attachments/assets/6777faed-14fe-4bb3-8dee-20f2ff865d86" />
<ul>
  <li><strong>First Submission:</strong> 2021-03-22 19:56:20 UTC</li>
  <li><strong>Last Submission:</strong> 2026-10-08 05:48:01 UTC</li>
  <li><strong>Last Analysis:</strong> 2026-10-08 05:48:01 UTC</li>
  <li><strong>Serving IP:</strong> 195.24.68.4</li>
  <li><strong>Status Code:</strong> 200</li>
  <li><strong>Content-Type:</strong> image/png</li>
  <li><strong>Network Requests:</strong> 2 HTTP/HTTPS transactions observed</li>
</ul>
<blockquote>
<strong>Finding:</strong> The URL has been present in VirusTotal since <strong>2021</strong> and was analyzed again on <strong>2026-10-08</strong>. It was observed resolving to <strong>195.24.68.4</strong> and returned an <strong>HTTP 200</strong> response with <strong>image/png</strong> content. The same URL was also observed in both HTTP and HTTPS transactions.
</blockquote>
<h3>🔗 Step 3 — Evidence Correlation & Impact Check</h3>

<h6>SOC L1 Thinking</h6>

<blockquote>
The URL was identified as malicious, so I will check the endpoint for any related activity and take containment action if required.
</blockquote>

<h4>1. Endpoint Investigation & Containment</h4>

<p>The endpoint was <strong>contained</strong> in EDR. The available browser history did not contain the alerted <strong>mogagrocol.ru</strong> URL, while the Proxy log had already recorded a request to the URL.</p>
<img width="1594" height="767" alt="image" src="https://github.com/user-attachments/assets/f4ba5528-f8de-490c-9d0f-9b0d14494079" />
<blockquote>
<strong>Finding:</strong> The host was contained. Although the alerted URL was not present in the available EDR browser history, the Proxy log confirms that a request to the URL was observed from the endpoint.
</blockquote>
<h3>⚖️ Step 4 — TP/FP, Severity & MITRE Mapping</h3>

<h6>SOC L1 Thinking</h6>

<blockquote>
The URL was flagged as malicious by multiple security vendors and the request was confirmed in the Proxy log. With the endpoint contained, I can now classify the alert, assess its severity, and map the activity to the relevant MITRE ATT&CK technique.
</blockquote>

<h4>1. Alert Verdict & Severity</h4>

<ul>
  <li><strong>Verdict:</strong> True Positive</li>
  <li><strong>Severity:</strong> High</li>
</ul>

<!-- LetsDefend final result screenshot here -->

<h4>2. MITRE ATT&CK Mapping</h4>

<ul>
  <li><strong>Technique:</strong> Phishing</li>
  <li><strong>MITRE ATT&CK ID:</strong> T1566</li>
</ul>

<blockquote>
<strong>Finding:</strong> The alert is confirmed as a <strong>True Positive</strong> with <strong>High</strong> severity. The activity is mapped to <strong>T1566 — Phishing</strong> based on the confirmed malicious phishing URL.
</blockquote>

<h3>🚨 Step 5 — Action</h3>

<h6>SOC L1 Thinking</h6>

<blockquote>
The alert was confirmed as a True Positive, the endpoint was contained, and the required investigation was completed. I can now close the alert after documenting the findings.
</blockquote>

<h4>1. Alert Closure</h4>
<img width="1596" height="589" alt="image" src="https://github.com/user-attachments/assets/0f38774e-7d74-447d-871c-8e36ec2bf6e1" />
<blockquote>
<strong>Action:</strong> Alert closed as <strong>True Positive</strong> after investigation and endpoint containment.
</blockquote>
