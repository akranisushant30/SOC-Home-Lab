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
<h4>VirusTotal Analysis</h4>

<p>I checked the attachment on VirusTotal and found that multiple vendors detected it as a Trojan, Phishing, or Downloader. Some detections also pointed to the <code>CVE-2017-11882</code> exploit. DOCGuard also marked the file as <strong>MALWARE</strong>.</p>
<img width="1866" height="874" alt="image" src="https://github.com/user-attachments/assets/57f08d5d-d6cf-4d20-9e4f-20798698b51b" />
