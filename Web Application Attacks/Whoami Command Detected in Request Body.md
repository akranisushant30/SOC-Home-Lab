<h2>🔎 Investigation Overview</h2>
A web attack alert was triggered on <code>WebServer1004</code> because an HTTP POST request contained the string <code>whoami</code>. The request was allowed, so further investigation is required to determine whether command execution occurred.
<h3>🚨 Step 1 — Alert Triage &amp; Scope</h3>

<h6>🧠 SOC L1 Thinking</h6>
<blockquote><p>Before investigating further, I need to understand why the alert was triggered and identify the source and destination of the traffic.</p></blockquote>
<h4>1. Alert Review</h4>
<img width="1553" height="519" alt="image" src="https://github.com/user-attachments/assets/1527fdc5-5fee-4b9c-ad98-f7097dbd3f99" />
<p>The alert was triggered because the HTTP POST request body contained the string <code>whoami</code>. The request was allowed and traffic originated from <code>61.177.172.87</code> and targeted <code>WebServer1004 (172.16.17.16)</code>.</p>
<h4>2. Collect Data</h4>
<blockquote><p>I'll check the source IP's ownership and reputation, along with the available details of the target server.
</p></blockquote>
<h5>Source IP Ownership Check - Whois IP 61.177.172.87</h5>
<img width="762" height="499" alt="image" src="https://github.com/user-attachments/assets/15042235-82b9-4538-a8d1-3a23856bd2a0" />
<p>The source IP belongs to China Telecom (CHINANET-JS), registered under APNIC.</p>
<h5>Source IP Reputation Check</h5>
<img width="1301" height="562" alt="image" src="https://github.com/user-attachments/assets/dfaa1fa9-30bd-42b3-8e21-493930c79cfc" />
<p>VirusTotal flagged the source IP <code>61.177.172.87</code> as malicious or suspicious across multiple security vendors.</p>
<h3>🔍 Step 2 — Relevant Log Analysis</h3>
<h6>🧠 SOC L1 Thinking</h6>
<blockquote>
<p>I need to examine the HTTP request details to determine whether it contains a command injection attempt.</p></blockquote>
<h4>1. Examine HTTP Traffic</h4>
<img width="1255" height="423" alt="image" src="https://github.com/user-attachments/assets/0f6376da-9a52-487d-9dd8-ac586bd0c68c" />
<p>The source IP sent multiple POST requests to <code>/video/</code> using the same outdated Internet Explorer user-agent. The requests contained commands such as <code>ls</code>, <code>whoami</code>, <code>uname</code>, <code>cat /etc/passwd</code>, and <code>cat /etc/shadow</code>. All requests were permitted and returned HTTP 200 responses. This pattern suggests an attempt to execute system commands and access sensitive system files on the target server.</p>
<h4>Findings</h4>
<blockquote>
<p>HTTP traffic contained multiple system commands targeting the web server. The requests were permitted and returned HTTP 200 responses.</p></blockquote>
<h3>🔎 Step 3 — Evidence Correlation &amp; Impact Assessment</h3>

<h6>🧠 SOC L1 Thinking</h6>
<blockquote>
<p>Since the source IP has a suspicious reputation and the HTTP requests contain multiple system commands, I need to correlate these findings to determine the potential impact on the target server.</p></blockquote>
<ul>
<li><strong>Traffic:</strong> Malicious</li>
<li><strong>Attack Type:</strong> Command Injection</li>
<li><strong>Planned Test:</strong> No evidence found</li>
<li><strong>Traffic Direction:</strong> Internet → Company Network</li>
</ul>
<h4>Attack Success Verification</h4>
<img width="1565" height="738" alt="image" src="https://github.com/user-attachments/assets/abfe5dbd-d2b7-49ee-8f20-dc5e43c2f756" />
<p>I checked the command history in Endpoint Security on <code>WebServer1004</code> and found the same commands observed in the HTTP traffic, confirming that command execution occurred on the server.</p>

<h4>Findings</h4>
<blockquote>
<p>The investigation confirmed successful command execution on the target server, indicating a successful Command Injection attack.</p></blockquote>

<h3>⚖️ Step 4 — Attack Classification &amp; MITRE ATT&amp;CK Mapping</h3>

<h6>🧠 SOC L1 Thinking</h6>
<blockquote>
<p>Since command execution was confirmed on the target server, I need to classify the alert and map the activity to the relevant MITRE ATT&amp;CK technique.</p></blockquote>
<ul>
<li><strong>Alert Classification:</strong> True Positive</li>
<li><strong>Attack Type:</strong> Command Injection</li>
<li><strong>MITRE ATT&amp;CK:</strong> T1190 — Exploit Public-Facing Application</li>
</ul>
<img width="1718" height="332" alt="image" src="https://github.com/user-attachments/assets/7472e530-2eef-4908-af95-156a7a598326" />
<h4>Add Artifacts</h4>
<ul>
<li><strong>Value:</strong> 61.177.172.87</li>
<li><strong>Type:</strong> IP Address</li>
<li><strong>Comment:</strong> Malicious source IP associated with the attack.</li>
</ul>
<h4>Findings</h4>
<blockquote><p>The alert was classified as a True Positive. Command execution was confirmed on the target server, indicating a successful Command Injection attack.</p></blockquote>
<h3>🛡️ Step 5 — Response &amp; Escalation</h3>
<h4>SOC L1 Thinking</h4>
<blockquote><p>Since the attack was successful, I need to escalate the incident to Tier 2 and take appropriate containment measures as per SOC procedures.</p></blockquote>
<h4>Containment</h4>
<p>I isolated <code>WebServer1004</code> from the network to prevent further malicious activity and limit the impact of the attack.</p>
<img width="1529" height="750" alt="image" src="https://github.com/user-attachments/assets/e13254a9-25fc-47bf-a175-18e090fcc30f" />
<h4>Tier 2 Escalation</h4>
<p>Escalation Required: Yes</p>
<p>Reason: Successful command execution was confirmed on the target server.</p>
