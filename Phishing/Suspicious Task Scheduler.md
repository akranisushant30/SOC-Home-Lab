<h2>🔎 Investigation Phase</h2>

<p>A <strong>Medium-severity phishing email alert</strong> was generated for an email with the subject <strong>COVID19 Vaccine</strong>. The alert was triggered by <strong>SOC140 - Phishing Mail Detected - Suspicious Task Scheduler</strong>, and the device action was recorded as <strong>Blocked</strong>.</p>
<img width="1581" height="432" alt="image" src="https://github.com/user-attachments/assets/12bc90e8-2bbd-4bdf-b307-bd762d799d1e" />

<p>The investigation will focus on checking the email details, identifying what made it suspicious, and verifying whether any related activity occurred.</p>
<h3>🚨 Step 1 — Alert Triage & Scope</h3>

<h6>SOC L1 Thinking</h6>

<blockquote>
The alert indicates a potentially suspicious email, but I need to understand the basic details before investigating further. I will review the sender, recipient, source address, and blocking status to establish the scope of the alert.
</blockquote>
<h4>1. Parse Email</h4>

<p>The email details were reviewed in Mail Security to identify the sender, recipient, message content, and attachment.</p>
<img width="1756" height="571" alt="image" src="https://github.com/user-attachments/assets/014f887b-b53a-424d-869d-fe1ff2f4f35d" />
<ul>
  <li><strong>Date:</strong> 2021-03-21 14:56:57</li>
  <li><strong>SMTP Address:</strong> 189.162.189.159</li>
  <li><strong>Sender:</strong> aaronluo@cmail.carleton.ca</li>
  <li><strong>Recipient:</strong> mark@letsdefend.io</li>
  <li><strong>Subject:</strong> COVID19 Vaccine</li>
</ul>
<blockquote>
<strong>Step 1 Finding:</strong> The email was sent from <strong>aaronluo@cmail.carleton.ca</strong> to <strong>mark@letsdefend.io</strong> with the subject "COVID19 Vaccine". The message urges the recipient to open it and includes a password-protected attachment. These details make the email suspicious and require further investigation.
</blockquote>
<h3>🔎 Step 2 — Relevant Log Analysis</h3>

<h6>SOC L1 Thinking</h6>

<blockquote>
The email contains suspicious content and a password-protected attachment. I will review the related Exchange logs to check whether the sender's network activity matches the email details.
</blockquote>
<h4>1. Exchange Log Analysis</h4>

<p>Log Management returned an Exchange event showing communication from the sender IP to the mail server.</p>
<img width="1545" height="544" alt="image" src="https://github.com/user-attachments/assets/8721bb5c-ec86-49fc-b7db-33610d7542cc" />

<ul>
  <li><strong>Source IP:</strong> 189.162.189.159</li>
  <li><strong>Source Port:</strong> 49371</li>
  <li><strong>Destination IP:</strong> 172.16.20.3</li>
  <li><strong>Destination Port:</strong> 25 (SMTP)</li>
  <li><strong>Event Time:</strong> 2021-03-21 14:36:51</li>
</ul>

<blockquote>
<strong>Finding:</strong> The Exchange log shows SMTP communication from 189.162.189.159 to the mail server at 172.16.20.3. The source IP matches the sender IP in Mail Security, but the timestamps differ, so this log alone does not confirm the exact email transaction.
</blockquote>
<h3>🔗 Step 3 — Evidence Correlation & Impact Check</h3>

<h6>SOC L1 Thinking</h6>

<blockquote>
The email contains suspicious content and a password-protected attachment. I will check the attachment's reputation and correlate the results with the email findings to determine whether it is potentially malicious.
</blockquote>
<h4>1. VirusTotal — Attachment Detection</h4>

<p>The email attachment was analyzed using VirusTotal to review its detection results.</p>

<img width="1881" height="938" alt="image" src="https://github.com/user-attachments/assets/1d1fba03-b730-499d-9f6b-ff770f1723e1" />
<ul>
  <li><strong>File Type:</strong> PDF</li>
  <li><strong>Threat Categories:</strong> Trojan, Downloader, Phishing/Fraud</li>
  <li><strong>Detection Results:</strong> Multiple security vendors flagged the attachment as malicious.</li>
</ul>
<blockquote>
<strong>Step 3 Finding:</strong> VirusTotal analysis showed that multiple security vendors detected the attachment as malicious, with classifications including Trojan, Downloader, and Phishing/Fraud.
</blockquote>
<h3>⚖️ Step 4 — Assessment & MITRE Mapping</h3>

<h6>SOC L1 Thinking</h6>

<blockquote>
The attachment was flagged as malicious by multiple security vendors, and the email was blocked before delivery. I will assess the alert using the available evidence, determine what can be concluded, and document any unverified activity separately.
</blockquote>
<h4>1. Alert Assessment</h4>
<img width="1590" height="557" alt="image" src="https://github.com/user-attachments/assets/680fcfce-d644-4636-807b-0cf9625d483f" />
<h4>2. MITRE ATT&amp;CK Mapping</h4>

<ul>
  <li><strong>Tactic:</strong> Initial Access</li>
  <li><strong>Technique:</strong> Phishing (T1566)</li>
</ul>

<p>The email and attachment are consistent with a phishing attempt. However, the available evidence does not confirm scheduled task creation or execution on the recipient's system.</p>

<h4>3. Assessment Summary</h4>
<img width="1422" height="200" alt="image" src="https://github.com/user-attachments/assets/a25fefb8-6371-404c-acb1-7514c6c6ce2e" />

<blockquote>
The email was blocked before delivery, and VirusTotal detections support the malicious classification of the attachment. LetsDefend recorded the final result as False Positive, but the reason for that classification could not be verified from the available evidence.
</blockquote>
<h3>🛡️ Step 5 — Action</h3>

<h6>SOC L1 Thinking</h6>

<blockquote>
The email was blocked before delivery. I will document the findings and recommend a review of the alert's final classification.
</blockquote>

<blockquote>
<strong>Final Action:</strong> The investigation findings were documented, and the alert was recommended for further review due to the malicious attachment detections.
</blockquote>
