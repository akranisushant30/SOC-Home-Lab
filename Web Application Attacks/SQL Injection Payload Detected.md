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
<h4>2. Collect Data</h4>

<blockquote>
I'll check the source IP's ownership and reputation, along with the available details of the target server.
</blockquote>
