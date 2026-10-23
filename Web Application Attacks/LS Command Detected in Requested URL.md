<h2>🔎 Investigation Phase</h2>
<p>I received a High-severity alert on `EliotPRD` because the requested URL contained the string `ls`. Since the request was allowed, I need to check whether it was a normal search request or something suspicious.</p>
<h3>🚨 Step 1 — Alert Triage &amp; Scope</h3>
<h4>SOC L1 Thinking</h4>
<blockquote><p>I will start by reviewing the alert rule and examining the traffic details to understand what triggered the detection and which devices were involved.</p></blockquote>
<h4>1. Alert Review</h4>
<img width="1358" height="585" alt="image" src="https://github.com/user-attachments/assets/0b4629e1-19e9-446d-a047-5fe6d5e80318" />
<p>Here, the alert was triggered because the URL contains the string <code>ls</code>. The GET request was allowed and was associated with the host <code>EliotPRD</code>.</p>
<h4>2. Collect Data</h4>
<blockquote>
<p>First, I'll gather information about the source IP's & Destination IP's ownership and reputation.</p>
</blockquote>
<h6>Source IP Ownership Check - Whois 172.16.17.46</h6>
<img width="802" height="456" alt="image" src="https://github.com/user-attachments/assets/d4af17f3-41c1-46f1-8a90-55a67249c1dd" />
<p>First, I checked the IP address in our internal network and found that it was assigned to the device <code>EliotPRD</code>, which was used by the user <code>eliot</code>.</p>
