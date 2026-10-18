<h2>🔎 Investigation Phase</h2>
<p>I received a Medium-severity alert for JavaScript code detected in a requested URL on <code>WebServer1002</code>. The request was allowed, so I need to investigate whether this was an attempt to exploit the web application and check if there are any signs of a successful attack.</p>
<h3>🚨 Step 1 — Alert Triage &amp; Scope</h3>

<h4>🧠 SOC L1 Thinking</h4>

<p>First, I'll review the alert to understand why it was triggered and what I need to investigate next.</p>

<h4>1. Alert Review</h4>
<img width="1555" height="464" alt="image" src="https://github.com/user-attachments/assets/f8fc81b8-0971-486d-8cf2-fee1f9af0b02" />
<p>The rule detected JavaScript code in the requested URL. This could indicate an XSS attempt, so I'll first understand the request and identify the traffic source and destination before moving further with the investigation.</p>

<h4>2. Collect Data</h4>
<blockquote><p>I'll start by checking the source IP to identify its owner and reputation.</p></blockquote>
<h6>Source IP Ownership Check - Whois IP 112.85.42.13</h6>
<img width="769" height="883" alt="image" src="https://github.com/user-attachments/assets/e9705d27-b12e-4dc8-b4fc-f45e96909d0e" />
<p>It belongs to the <strong>China Unicom Jiangsu Province network</strong> (AS4837), registered under APNIC. The allocated network range is <code>112.80.0.0/13</code>.</p>
<h6>Source IP Reputation Check</h6>
<img width="1334" height="876" alt="image" src="https://github.com/user-attachments/assets/48cc2cdf-6430-42fc-843b-d4fd6986c36d" />
<p>I checked the source IP on SOCradar and found that four threat-intelligence feeds had flagged it. This suggests the IP has been reported for suspicious activity.</p>

<h4>📝 Step 1 Findings</h4>
<blockquote>
<p>The source IP belongs to a network in China and has been flagged by multiple threat-intelligence feeds for suspicious activity. I'll continue by checking the web server logs to understand how the request was handled.</p></blockquote>
<h3>🚨 Step 2 — Relevant Log Analysis</h3>
<h4>🧠 SOC L1 Thinking</h4>
<blockquote>
<p>Now that I've checked the source IP's reputation, I'll look at the HTTP traffic to see what was sent to the web server and whether the request contains anything suspicious.</p>
</blockquote>
<h4>1. Examine HTTP Traffic</h4>
<p>I found multiple firewall events from <code>112.85.42.13</code> to <code>172.16.17.17:443</code></p>
<img width="1745" height="664" alt="image" src="https://github.com/user-attachments/assets/a44fb3c2-2263-4b66-b0c4-5eccd42ba5fe" />
<p>These requests were permitted by the security device, but returned HTTP 302 responses with a response size of 0. This suggests the requests were redirected or handled without a response body.</p>
<h4>📝 Findings</h4>
<blockquote>
<p>I found several requests from the same IP containing XSS payloads. The requests were allowed, but they returned HTTP 302 with no response body. This looks like an attempt to test for XSS, although I couldn't confirm whether any payload was successfully executed.</p>
</blockquote>

<h3>Step 3 — Evidence Correlation &amp; Impact Check</h3>

<h4>🧠 SOC L1 Thinking</h4>
<blockquote>
<p>Now that I've identified repeated XSS payloads, I'll check whether there's any evidence that the requests affected the web server or successfully executed.</p></blockquote>

<h4>🔎 Investigation</h4>

<ul>
  <li><b>Attack Type:</b> Cross-Site Scripting (XSS)</li>
  <li><b>Planned Test:</b> No planned test email or attack simulation hostname was found.</li>
  <li><b>Traffic Direction:</b> Internet → Company Network</li>
  <li><b>Attack Successful:</b> No evidence of successful JavaScript execution was found. The requests returned HTTP 302 with a response size of 0.</li>
</ul>

<h4>📝 Findings</h4>

<p>The external IP sent multiple XSS payloads to the web server. No evidence of a planned test or successful payload execution was found. Based on the available logs, this appears to be an unsuccessful XSS attempt.</p>

<h3>Step 4 — Assessment &amp; MITRE Mapping</h3>

<h4>🧠 SOC L1 Thinking</h4>

<p>Based on the evidence, I'll classify the alert and document the relevant MITRE ATT&amp;CK technique.</p>
<ul>
  <li><b>MITRE ATT&amp;CK:</b> T1190 — Exploit Public-Facing Application (as mapped by the alert).</li>
</ul>
<img width="1547" height="465" alt="image" src="https://github.com/user-attachments/assets/c493365b-2299-4034-966a-8c889f33e7e5" />
<h4>📝 Findings</h4>
<blockquote>
<p>I classified this as a True Positive because the alert detected genuine XSS-related activity. However, the available logs do not show that the payloads executed successfully, so I found no confirmed evidence of compromise.</p></blockquote>
<h3>Step 5 — Action</h3>
<p>Tier 2 escalation was not required because the internet-originated attack was unsuccessful. I submitted the case with the final verdict.</p>


