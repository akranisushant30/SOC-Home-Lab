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

