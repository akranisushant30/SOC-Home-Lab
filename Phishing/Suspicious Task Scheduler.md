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
