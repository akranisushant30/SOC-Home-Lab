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
