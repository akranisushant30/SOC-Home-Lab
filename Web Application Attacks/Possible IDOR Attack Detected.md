<h2>🔎 Investigation Overview</h2>
<p>I received a Medium-severity alert for a possible IDOR attack on <code>WebServer1005</code>. The alert was triggered by repeated POST requests to the <code>/get_user_info/</code> endpoint. I will check the request details to understand what happened.</p>
<h3>🚨 Step 1 — Alert Triage &amp; Scope</h3>
<h4>🧠 SOC L1 Thinking</h4>
<blockquote><p>I will review the alert details and check the source and destination information to understand what triggered the alert.</p></blockquote>
<h4>1. Alert Review</h4>
<img width="1569" height="527" alt="image" src="https://github.com/user-attachments/assets/95805efb-c6bf-4ff4-ba04-79d764c3c9e7" />
<p>The alert was triggered due to repeated POST requests to the same page, <code>/get_user_info/</code>. The requests were allowed on <code>WebServer1005</code>. I will collect additional information to investigate the alert further.</p>
