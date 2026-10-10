<img width="1314" height="580" alt="image" src="https://github.com/user-attachments/assets/82a5bc59-547a-416a-9e3d-2646c094bf8b" /><h2>🔎 Investigation Phase</h2>

<p>A <strong>Medium-severity phishing email alert</strong> was generated for an internal email sent from <strong>john@letsdefend.io</strong> to <strong>susie@letsdefend.io</strong> with the subject <strong>Meeting</strong>. The alert was triggered by <strong>SOC120 - Phishing Mail Detected - Internal to Internal</strong>, and the device action was recorded as <strong>Allowed</strong>.</p>

<p>The investigation will focus on reviewing the email content, checking for suspicious attachments or links, and determining whether the message poses a security risk.</p>
<img width="1332" height="489" alt="image" src="https://github.com/user-attachments/assets/ef993c7c-57dd-415e-97fb-7949e4c5c92d" />
<h3>🚨 Step 1 — Alert Triage & Scope</h3>

<h6>SOC L1 Thinking</h6>

<blockquote>
Before investigating the alert, I will review the email details, including its timestamp, SMTP address, sender, recipient, message content, and attachments. This will help me understand the alert and identify anything suspicious.
</blockquote>
<h4>1. Email Investigation</h4>

<p>I filtered the Mail Security logs using the sender IP and subject to locate the email associated with the alert.</p>
<img width="1341" height="396" alt="image" src="https://github.com/user-attachments/assets/46ed163e-38f1-4c98-b058-7a5abf7f661b" />
<p>However, the alert timestamp is <strong>2021-02-07 04:24:09 (+03:00)</strong>, while the email record shows <strong>2021-02-07 06:54:09</strong>. These timestamps differ by 2 hours and 30 minutes, so the time correlation needs to be verified before confirming an exact match.</p>

<ul>
  <li><strong>Date:</strong>2021-02-07 06:54:09</li>
  <li><strong>SMTP Address:</strong> 172.16.20.3</li>
  <li><strong>Sender Address:</strong> john@letsdefend.io</li>
  <li><strong>Recipient Address:</strong> susie@letsdefend.io</li>
  <li><strong>Is the mail content suspicious?</strong> No obvious suspicious content identified from the message body.</li>
  <li><strong>attachments or URLs?</strong> No.</li>
</ul>
<h4>Step 1 Finding</h4>

<blockquote>
A matching email was found using the sender IP and subject filters. The sender IP matches the alert, but the timestamp difference and conflicting attachment information require further investigation before determining whether the alert is a false positive.
</blockquote>
<h3>🔎 Step 2 — Relevant Log Analysis</h3>

<h6>SOC L1 Thinking</h6>
<blockquote>
Since the sender IP matches the alert but the timestamp and attachment details are inconsistent, I will check the Exchange logs to verify the email activity.
</blockquote>
<h4>1. Exchange Log Analysis</h4>

<p>I searched the Exchange logs and found an event showing communication from <strong>172.16.17.82</strong> to the mail server <strong>172.16.20.3</strong> over SMTP port 25.</p>
<img width="1314" height="580" alt="image" src="https://github.com/user-attachments/assets/f784a138-2bf1-4dfd-81c1-c0cf0b37a962" />
<blockquote>
<strong>Finding:</strong> The Exchange log shows SMTP traffic to the mail server at 172.16.20.3. The event occurred 18 seconds before the email record, assuming both timestamps use the same timezone. The source IP is 172.16.17.82, so the log alone does not identify the sender's device or confirm successful email delivery.
</blockquote>
<h3>🔗 Step 3 — Evidence Correlation & Impact Check</h3>

<blockquote>
The email contains a normal meeting request between two internal users. No attachment, URL, or suspicious activity was found in the available evidence. Nothing reviewed so far indicates a phishing attempt.
</blockquote>
<h3>🧾 Step 4 — Assessment</h3>

<blockquote>
The email appears to be a normal meeting request. I found no attachment, URL, or other suspicious activity in the logs I checked. Based on the available evidence, I marked the alert as a False Positive.
</blockquote>
<img width="865" height="438" alt="image" src="https://github.com/user-attachments/assets/e9aa55ac-9233-47a6-9c67-7151ffd23dab" />
<ul>
  <li><strong>Verdict:</strong> False Positive</li>
  <li><strong>MITRE ATT&CK:</strong> Not applicable</li>
</ul>
<h3>✅ Step 5 — Action</h3>

<blockquote>
The alert was marked as a False Positive because no clear signs of phishing were found. No further escalation was needed based on the available evidence.
</blockquote>
