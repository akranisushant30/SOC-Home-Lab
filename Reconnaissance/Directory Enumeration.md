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
<h3>3️⃣ Verify Discovered Resource — <code>/php.ini</code></h3>

<p align="justify">
Gobuster identified <code>/php.ini</code> with an <strong>HTTP 200</strong> response.
Because this file is related to PHP configuration, I manually verified the resource
to determine whether it was actually readable and whether it exposed configuration
information.
</p>

<h4>▶️ Command Used</h4>

<pre><code>curl http://192.168.67.128:8080/php.ini</code></pre>

<h4>🔍 Analysis</h4>

<p align="justify">
The request successfully returned the contents of the file, confirming that
<code>/php.ini</code> was publicly accessible from the attacker machine.
The file exposed PHP-related configuration values including
<code>magic_quotes_gpc</code>, <code>allow_url_fopen</code>, and
<code>allow_url_include</code>.
</p>

<p align="justify">
At this stage, the finding is treated as <strong>configuration information exposure</strong>.
The exposed values provide additional information about the application's PHP
environment, but no exploitation or system compromise was performed during this step.
</p>

<blockquote>
<strong>📌 Finding:</strong><br>
The <code>/php.ini</code> resource was successfully accessed and returned
PHP configuration information, confirming that the Gobuster discovery was valid.
</blockquote>

<hr>

<h3>4️⃣ Verify <code>/robots.txt</code></h3>

<p align="justify">
Gobuster also discovered <code>/robots.txt</code> with an
<strong>HTTP 200</strong> response. I manually reviewed the file to check whether
it disclosed any additional directories or paths that were excluded from web crawlers.
</p>

<h4>▶️ Command Used</h4>

<pre><code>curl http://192.168.67.128:8080/robots.txt</code></pre>

<h4>🔍 Analysis</h4>

<p align="justify">
The <code>robots.txt</code> file was publicly accessible, but the
<code>Disallow</code> directive was empty. Therefore, the file did not reveal
any additional hidden or restricted directories for further enumeration.
</p>

<blockquote>
<strong>📌 Finding:</strong><br>
The <code>robots.txt</code> resource was accessible, but it did not expose
any additional paths that required further verification.
</blockquote>

<hr>

<h3>🎯 Attack Phase Result</h3>

<p align="justify">
The directory enumeration successfully identified multiple web resources on the
target application. Manual verification confirmed that <code>/php.ini</code>
exposed PHP configuration information, while <code>/robots.txt</code> did not
reveal any additional paths.
</p>
<img width="1200" height="800" alt="image" src="https://github.com/user-attachments/assets/741254da-7414-4dc0-9352-b489b5b994af" />
