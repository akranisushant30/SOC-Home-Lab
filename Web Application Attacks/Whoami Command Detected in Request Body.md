<h2>🔎 Investigation Overview</h2>
A web attack alert was triggered on <code>WebServer1004</code> because an HTTP POST request contained the string <code>whoami</code>. The request was allowed, so further investigation is required to determine whether command execution occurred.
<h3>🚨 Step 1 — Alert Triage &amp; Scope</h3>

<h6>🧠 SOC L1 Thinking</h6>
<blockquote><p>Before investigating further, I need to understand why the alert was triggered and identify the source and destination of the traffic.</p></blockquote>
<h4>1. Alert Review</h4>
<img width="1553" height="519" alt="image" src="https://github.com/user-attachments/assets/1527fdc5-5fee-4b9c-ad98-f7097dbd3f99" />
<p>The alert was triggered because the HTTP POST request body contained the string <code>whoami</code>. The request was allowed and traffic originated from <code>61.177.172.87</code> and targeted <code>WebServer1004 (172.16.17.16)</code>.</p>
