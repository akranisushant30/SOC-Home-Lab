<h2>🔎 Investigation Overview</h2>
<p>I received a Medium-severity alert for a possible IDOR attack on <code>WebServer1005</code>. The alert was triggered by repeated POST requests to the <code>/get_user_info/</code> endpoint. I will check the request details to understand what happened.</p>
<h3>🚨 Step 1 — Alert Triage &amp; Scope</h3>
<h4>🧠 SOC L1 Thinking</h4>
<blockquote><p>I will review the alert details and check the source and destination information to understand what triggered the alert.</p></blockquote>
<h4>1. Alert Review</h4>
<img width="1569" height="527" alt="image" src="https://github.com/user-attachments/assets/95805efb-c6bf-4ff4-ba04-79d764c3c9e7" />
<p>The alert was triggered due to repeated POST requests to the same page, <code>/get_user_info/</code>. The requests were allowed on <code>WebServer1005</code>. I will collect additional information to investigate the alert further.</p>
<h4>2. Collect Data</h4>
<blockquote><p>I will gather information about the source IP address, its ownership, and reputation to better understand the traffic and investigate the alert.</p></blockquote>
<h6>Source IP Ownership Check - Whois 134.209.118.137</h6>
<img width="772" height="679" alt="image" src="https://github.com/user-attachments/assets/5a1d95ed-941a-4067-98a4-0b3e0f10348e" />
<p>The IP belongs to DigitalOcean, LLC located at United States and the ASN is AS14061.</p>
<h6>Source IP Reputation Check - 134.209.118.137</h6>
<img width="1838" height="514" alt="image" src="https://github.com/user-attachments/assets/9b64554f-af00-4ab6-b5f8-2dce1b5f3c1f" />
<p>I checked the IP on VirusTotal and found 1 vendor flagged it as malicious, with a community score of -6.</p>
<h2>🔍 Step 2: Relevant Log Analysis</h2>
<h3>🧠 SOC L1 Thinking</h3>
<blockquote><p> I will now examine the relevant HTTP logs to check whether the repeated POST requests contain suspicious parameters or signs of an attempt to access another user's information.</p></blockquote>
<h4>1. HTTP Log Analysis</h4>
<img width="1758" height="545" alt="image" src="https://github.com/user-attachments/assets/58adccbf-a715-4e58-b46b-b0725a4d5b57" />
<p>There were multiple POST requests to the same page with different ID values in the parameters. All requests were permitted and returned HTTP 200 responses. This may indicate an attempt to access multiple users information, so further investigation is needed to determine whether unauthorized data was exposed.</p>
<h2>🔗 Step 3: Correlation & Impact</h2>
<h3>🧠 SOC L1 Thinking</h3>
<blockquote><p>I will check whether this activity was part of a planned security test and look for any related evidence to understand its impact.</p></blockquote>
<p><strong>Planned Test:</strong> Not Planned</p>
<img width="1771" height="488" alt="image" src="https://github.com/user-attachments/assets/e800b471-d4b3-4bf1-91ba-24be4e0a0005" />
<p>I checked the response sizes for different <code>user_id</code> values. The responses varied in size, which may indicate that some information was returned.</p>
<p><strong>Result:</strong> Attack Successful</p>
<h2>⚖️ Step 4: Assessment</h2>
<p><strong>Verdict:</strong> True Positive</p>
<img width="1544" height="329" alt="image" src="https://github.com/user-attachments/assets/24b8f6fc-81bd-4398-82b2-3a7d003381c1" />
<ul>
<li><strong>Is Traffic Malicious?</strong> Yes, suspicious activity consistent with a possible IDOR attempt.</li>
<li><strong>Attack Type:</strong> IDOR (Insecure Direct Object Reference)</li>
<li><strong>Traffic Direction:</strong> <code>134.209.118.137 → 172.16.17.15</code></li>
</ul>
<h2>🚨 Step 5: Action</h2>
<p>Since the alert was classified as a True Positive, I escalated it to Tier 2 for further investigation and blocked the source IP as a containment measure.</p>
<img width="1287" height="396" alt="image" src="https://github.com/user-attachments/assets/a925ab8c-3974-4daa-8651-de50dc65d4fd" />
