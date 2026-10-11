<h2>🔎 Investigation Phase</h2>

<p>I received a High-severity alert for an email with the subject <strong>Invoice</strong>, sent from <code>accounting@cmail.carleton.ca</code> to <code>richard@letsdefend.io</code>. The email was allowed, so I need to check whether the attachment is malicious.</p>
<img width="1552" height="402" alt="image" src="https://github.com/user-attachments/assets/76eda9f7-86cf-43c4-937f-21b4195db815" />

<h3>🚨 Step 1 — Alert Triage & Scope</h3>

<h6>SOC L1 Thinking</h6>

<blockquote>
I'll look for this email in the Mail Security logs and check the sender, email content, and attachment details.
</blockquote>


<h4>1. Email Investigation</h4>

<p>I searched the Mail Security logs using the sender address and subject and found the matching email.</p>
<img width="1553" height="500" alt="image" src="https://github.com/user-attachments/assets/5c87fc5e-7189-4bac-a714-5a82e5abeea8" />
<ul>
  <li><strong>From:</strong> accounting@cmail.carleton.ca</li>
  <li><strong>To:</strong> richard@letsdefend.io</li>
  <li><strong>Subject:</strong> Invoice</li>
  <li><strong>Sender IP:</strong> 49.234.43.39</li>
  <li><strong>Email Time:</strong> 2021-01-31 18:18:30</li>
  <li><strong>Action:</strong> Unknown</li>
  <li><strong>Attachment:</strong> ZIP file</li>
</ul>

<p>The sender IP matches the alert. However, the alert time is <code>15:48:30 +03:00</code>, while the email record shows <code>18:18:30</code> without a timezone. The alert action is <strong>Allowed</strong>, but the email record shows <strong>Unknown</strong>.</p>
<h3>🔎 Step 2 — Relevant Log Analysis</h3>

<h6>SOC L1 Thinking</h6>

<blockquote>
The sender IP matches the alert, but the timestamp and action are different in the email record. I'll check the Exchange logs for related activity and see if they help clarify these differences.
</blockquote>

<h4>Exchange Log Analysis</h4>
<p>
I found an Exchange log with the same sender IP. I'll check what this log tells me about the email activity.
</p>
<img width="1528" height="697" alt="image" src="https://github.com/user-attachments/assets/7420c115-722d-4b68-b796-3e11ef895794" />
<p>The log shows a connection from <code>49.234.43.39</code> to the mail server <code>172.16.20.3</code> on SMTP port 25. The source IP matches the email, and the log time is 26 seconds before the email record.</p>

<p>This looks related to the email I found. However, the log doesn't confirm whether the email was successfully delivered.</p>
<h4>Finding</h4>

<blockquote>
The sender IP and timing match the email activity closely. I haven't confirmed email delivery yet, so I'll keep that in mind during the investigation.
</blockquote>
<h3>🔗 Step 3 — Evidence Correlation & Impact Check</h3>

<h6>SOC L1 Thinking</h6>

<blockquote>
The sender IP matches the Exchange log, and the timestamps may also line up after accounting for the timezone. Since the email contains a ZIP attachment and the alert is about a malicious attachment, I'll check the available file analysis results before deciding whether the alert is genuine.
</blockquote>
<h4>1. VirusTotal — Detection Tab</h4>
<p>I checked the attachment on VirusTotal and found that multiple vendors detected it as a Trojan, Phishing, or Downloader. Some detections also pointed to the <code>CVE-2017-11882</code> exploit.</p>
<img width="1866" height="874" alt="image" src="https://github.com/user-attachments/assets/57f08d5d-d6cf-4d20-9e4f-20798698b51b" />
<h4>2. VirusTotal — Relations Tab</h4>
<p>I checked the Relations tab and found two URLs associated with the file. The main URL, <code>http://andaluciabeach.net/image/network.exe</code>, was flagged by 10 out of 91 security vendors.</p>
<img width="1835" height="306" alt="image" src="https://github.com/user-attachments/assets/5158bf20-92fd-49a3-a90d-64ea4aad85d5" />
<p>The URL returned HTTP status <code>401</code>. This result alone doesn't confirm whether anyone in our environment accessed it, so I'll check the Log Management records next.</p>
<h4>3. Log Management </h4>

<p>I searched for the suspicious URL and found a matching request from internal host <code>172.16.17.45</code> at <code>2021-01-31 18:45:45</code>.</p>

<img width="1552" height="715" alt="image" src="https://github.com/user-attachments/assets/28b2e7a0-ca99-4328-96da-cd30550e173e" />
<ul>
  <li><strong>Request:</strong> GET</li>
  <li><strong>Process:</strong> EQNEDT32.EXE</li>
  <li><strong>Parent Process:</strong> excel.exe</li>
  <li><strong>Destination IP:</strong> 5.135.143.133</li>
  <li><strong>Device Action:</strong> Allowed</li>
</ul>

<p>The request was allowed, and the process details link the activity to Excel and EQNEDT32.EXE. This confirms that the suspicious URL was accessed.</p>
<h4>Step 3 Finding</h4>
<blockquote>
Multiple vendors flagged the attachment as malicious. I also found a log showing that Excel's child process, EQNEDT32.EXE, accessed the suspicious URL, and the request was allowed. This confirms suspicious activity on the internal host
</blockquote>
<h3>🧾 Step 4 — Assessment & MITRE Mapping</h3>
<h6>SOC L1 Thinking</h6>

<blockquote>
After checking the email, VirusTotal results, and proxy logs, this doesn't look like a false alarm. I'll classify it as a True Positive. The next step is to deal with the malicious email and the affected host.
</blockquote>
<h4>Assessment</h4>

<ul>
  <li><strong>Verdict:</strong> True Positive</li>
  <li><strong>Reason:</strong> The attachment was flagged as malicious, and the logs show that the suspicious URL was accessed.</li>
  <li><strong>MITRE ATT&CK (Alert):</strong> T1598.001</li>
</ul>
<h3>✅ Step 5 — Action</h3>
<h6>SOC L1 Thinking</h6>
<blockquote>
Since the email contained a malicious attachment and the logs showed access to the suspicious URL, I'll follow the playbook to delete the email and contain the affected host.
</blockquote>
<h4>1. Email Removal</h4>

<p>I first deleted the malicious email from the recipient's mailbox as instructed in the playbook. This helps prevent the recipient from accessing the malicious attachment again from their mailbox.</p>
<img width="1546" height="272" alt="image" src="https://github.com/user-attachments/assets/26cfb77a-44a4-418f-8ced-b517079c3d34" />
<h4>2. EDR Host Investigation</h4>
<p>I checked the host's history in EDR and found the same suspicious URL that I had identified in VirusTotal and the proxy logs. This confirmed that the URL was also present in the host's activity.</p>
<img width="1542" height="744" alt="image" src="https://github.com/user-attachments/assets/b720a5c7-2826-49c3-bd05-31526633f81f" />
<p>After checking the host history, I reviewed the processes and found <code>excel.exe</code> and <code>EQNEDT32.EXE</code>. I had also seen <code>EQNEDT32.EXE</code> accessing the suspicious URL in the proxy logs.</p>
<img width="1549" height="728" alt="image" src="https://github.com/user-attachments/assets/1803b60a-add9-4008-a694-0129408a6c3f" />
<p>After reviewing all the findings, I decided to contain the affected host to prevent any further suspicious activity.</p>
<img width="1176" height="421" alt="image" src="https://github.com/user-attachments/assets/1ab24af4-b880-4f7d-8745-3757b8b4c3b6" />

