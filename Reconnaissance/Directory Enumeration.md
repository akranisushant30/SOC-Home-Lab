<h1 align="center"> Directory Enumeration with Gobuster</h1>
<h1 align="center">⚔️ Attack Phase</h1>
<p>
In this phase, directory and file enumeration was performed against the target web application using Gobuster. The goal was to discover directories, files, and web resources that are not directly visible through normal website navigation.
This type of reconnaissance helps an attacker understand the structure of a web application and identify exposed resources that may reveal useful information for further investigation.</p>
<hr>
<h3>1️⃣ Verify Target Web Application</h3>

<p align="justify">
Before starting directory enumeration, I first verified that the target web
application was reachable and responding to HTTP requests.
</p>

<h4>▶️ Command Used</h4>

<pre><code>curl -I http://192.168.67.128:8080</code></pre>
<blockquote>
<b>Finding:</b> The target web application was active and responding successfully,
confirming that it was ready for directory enumeration.
</blockquote>
<img width="1200" height="800" alt="image" src="https://github.com/user-attachments/assets/5c590e2f-b744-46ab-9b69-88b81dba21fa" />
<h3>2️⃣ Directory Enumeration Using Gobuster</h3>

<p align="justify">
After confirming that the web application was reachable, I used
<b>Gobuster</b> to enumerate directories and files on the target web application.
Gobuster tested common web resource names from a wordlist and checked the HTTP
response returned by the server.
</p>

<h4>▶️ Command Used</h4>

<pre><code>gobuster dir -u http://192.168.67.128:8080/ -w /usr/share/wordlists/dirb/common.txt</code></pre>
<p align="justify">
Gobuster completed all <b>4,613 wordlist entries</b> and identified several
existing directories and files. Some resources were directly accessible,
some redirected to another location, while others returned
<code>403 Forbidden</code>.
</p>

<p align="justify">
The most interesting result was <code>/php.ini</code>, which returned
<b>HTTP 200</b>. This means the resource was accessible and should be
examined further to determine what information it exposes.
</p>

<blockquote>
<b>Finding:</b> Directory enumeration successfully discovered multiple web
resources on the target application, including an accessible
<code>/php.ini</code> file that requires further verification.
</blockquote>
