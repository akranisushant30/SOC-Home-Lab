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
