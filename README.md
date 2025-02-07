# Nikto-Usage-Examples-and-Help-Details

Nikto is a versatile tool with many options. Below is a comprehensive guide on how to use it effectively.

---

### **Basic Syntax**
```bash
nikto [options]
```

### **Help Menu**
To view all available options and details, run:
```bash
nikto -H
```

---

### **Examples of Common Usage**

#### 1. **Basic Scan**
Scan a target URL or IP:
```bash
nikto -h http://example.com
```

#### 2. **SSL/HTTPS Scan**
Scan a secure (HTTPS) website:
```bash
nikto -h https://example.com
```

#### 3. **Port Scan**
Specify a particular port to scan:
```bash
nikto -h http://example.com -p 8080
```

#### 4. **Output Results to a File**
Save the scan results to a file:
```bash
nikto -h http://example.com -o results.txt
```

#### 5. **Output Results in Different Formats**
Save the results in specific formats:
- CSV:
  ```bash
  nikto -h http://example.com -o results.csv -Format csv
  ```
- JSON:
  ```bash
  nikto -h http://example.com -o results.json -Format json
  ```
- XML:
  ```bash
  nikto -h http://example.com -o results.xml -Format xml
  ```

#### 6. **Scan Multiple Hosts**
Scan multiple targets from a file:
```bash
nikto -h hosts.txt
```
Where `hosts.txt` contains a list of URLs or IPs, one per line.

#### 7. **Custom User-Agent**
Specify a custom User-Agent string for the scan:
```bash
nikto -h http://example.com -useragent "CustomUserAgent/1.0"
```

#### 8. **Using Proxies**
Run the scan through a proxy:
```bash
nikto -h http://example.com -useproxy http://proxy.example:8080
```

#### 9. **Scan Specific Server Headers**
Limit the scan to specific headers:
```bash
nikto -h http://example.com -Cgidirs /cgi-bin,/scripts
```

#### 10. **Evade Detection**
Use delay between requests to avoid detection:
```bash
nikto -h http://example.com -pause 5
```
This adds a 5-second delay between requests.

#### 11. **Specify Plugins**
Use specific plugins for advanced scanning:
```bash
nikto -h http://example.com -Plugins "headers,cookies"
```

#### 12. **Verbose Mode**
Enable verbose output for more details during the scan:
```bash
nikto -h http://example.com -v
```

#### 13. **Ignore Specific Checks**
Skip certain tests or checks:
```bash
nikto -h http://example.com -Tuning -x 2,3
```
Here, `-x 2,3` disables database-related and file upload vulnerabilities.

---

### **Nikto Options Reference**

Here’s a list of key options:

| Option         | Description                                                                 |
|----------------|-----------------------------------------------------------------------------|
| `-h`           | Target host (IP or URL).                                                   |
| `-p`           | Port to scan (default: 80 for HTTP).                                       |
| `-ssl`         | Force SSL scan.                                                            |
| `-o`           | Output results to a file.                                                 |
| `-Format`      | Format for output (txt, html, csv, xml, json).                             |
| `-Tuning`      | Specify scan tests (1=files, 2=DBs, 3=XSS, etc.).                         |
| `-Plugins`     | Use specific plugins.                                                     |
| `-useragent`   | Use a custom User-Agent string.                                           |
| `-useproxy`    | Specify a proxy server for the scan.                                      |
| `-v`           | Enable verbose output.                                                   |
| `-Version`     | Display Nikto version information.                                        |
| `-update`      | Update the Nikto database and plugins.                                    |

---

### **Tuning Scan Types**

To fine-tune which types of vulnerabilities are tested, use the `-Tuning` option:
- `0` - File/CGI checks.
- `1` - Interesting files.
- `2` - Database files.
- `3` - XSS vulnerabilities.
- `4` - Injection (SQL/Command).
- `5` - Remote file retrieval.
- `6` - Denial of Service.
- `7` - Remote shell vulnerabilities.
- `8` - Authentication bypass.
- `x` - Exclude specific tests.

Example: Scan for XSS and Injection only:
```bash
nikto -h http://example.com -Tuning 3,4
```

---

### **Updating Nikto**
To keep Nikto up to date with the latest vulnerability checks:
```bash
nikto -update
```

---

Here are some **advanced Nikto usage examples** for scenarios where more precise or sophisticated scanning techniques are required.

---

### **1. Full Scan with Multiple Options**
Perform a detailed scan with specific options enabled:
```bash
nikto -h http://example.com -p 443 -ssl -o full_scan.html -Format html -v
```
This performs:
- A scan on port `443` (HTTPS).
- Saves the output in an HTML file.
- Enables verbose output for detailed logs.

---

### **2. Scan with Authentication**
Perform a scan using **Basic Authentication** credentials:
```bash
nikto -h http://example.com -id username:password
```

#### Using Cookies for Session-Based Authentication:
If the website uses cookies for session tracking, you can include the cookie:
```bash
nikto -h http://example.com -C "PHPSESSID=abc123; logged_in=true"
```

---

### **3. Host Header Injection Scan**
Scan for vulnerabilities related to Host Header Injection:
```bash
nikto -h http://example.com -useragent "Host: evil.com"
```

---

### **4. Scan Behind a Proxy with Credentials**
If you need to scan through a proxy that requires authentication:
```bash
nikto -h http://example.com -useproxy http://proxyuser:proxypass@proxy.example.com:8080
```

---

### **5. Test Specific Plugins**
Run a scan with only specific plugins enabled (e.g., testing headers and cookies):
```bash
nikto -h http://example.com -Plugins headers,cookies
```

---

### **6. Advanced Tuning for Vulnerability Categories**
Scan for specific vulnerability types. For example:
- **Files** and **CGI** checks (`0`).
- **Injection flaws** like SQL or command injection (`4`).
- **XSS vulnerabilities** (`3`).

Example:
```bash
nikto -h http://example.com -Tuning 0,3,4
```

#### Exclude Certain Categories:
Exclude scanning for XSS (`3`) and remote file inclusion (`5`):
```bash
nikto -h http://example.com -Tuning -x 3,5
```

---

### **7. Evade IDS/IPS with Throttling**
Introduce random delays to evade detection systems:
```bash
nikto -h http://example.com -pause 10
```
This introduces a **10-second delay** between requests.

#### Randomized Delay:
```bash
nikto -h http://example.com -randomize
```

---

### **8. Use Custom Configurations**
Specify a custom configuration file for specialized scans:
```bash
nikto -config /path/to/custom.conf -h http://example.com
```

---

### **9. Multiple Host Scanning with Ports**
Scan a file of multiple hosts with specific ports:
```bash
nikto -h targets.txt -p 80,443,8080
```

Where `targets.txt` contains:
```
http://example1.com
http://example2.com
192.168.1.10
```

---

### **10. Blind Injection Testing**
For blind SQL injection or command injection, use specific tuning (`4`) and verbose output:
```bash
nikto -h http://example.com -Tuning 4 -v
```

---

### **11. Scan for Specific File Extensions**
Target specific file types (e.g., `.php` and `.asp`):
```bash
nikto -h http://example.com -findonly .php,.asp
```

---

### **12. Analyze Specific HTTP Methods**
Check for vulnerabilities in HTTP methods like `PUT`, `DELETE`, or `TRACE`:
```bash
nikto -h http://example.com -method PUT
```

---

### **13. Running Nikto in Docker**
If you prefer running Nikto in a containerized environment:
1. Pull the Nikto Docker image:
   ```bash
   docker pull sullo/nikto
   ```
2. Run Nikto in a container:
   ```bash
   docker run --rm sullo/nikto -h http://example.com
   ```

---

### **14. Scan for Specific Directories**
Focus on particular directories, such as `/admin` or `/cgi-bin`:
```bash
nikto -h http://example.com -Cgidirs /admin,/cgi-bin
```

---

### **15. Debug Mode for Troubleshooting**
If you suspect issues during the scan, use debug mode:
```bash
nikto -h http://example.com -d
```

---

### **16. Integrate with Metasploit**
Combine Nikto results with Metasploit for further exploitation:
1. Save the scan results as a Nmap-compatible file:
   ```bash
   nikto -h http://example.com -o nmap_results.xml -Format xml
   ```
2. Import the results into Metasploit:
   ```bash
   msfconsole
   db_import nmap_results.xml
   ```

---

### **17. Advanced SSL Analysis**
Perform an in-depth SSL/TLS analysis of the target:
```bash
nikto -h https://example.com -ssl
```

---

### **18. Exploit Specific Issues**
If Nikto identifies specific vulnerabilities, you can combine it with other tools, like `curl` or custom scripts, to verify or exploit those findings.

#### Example: Exploiting a File Upload Vulnerability
If Nikto identifies a vulnerable upload endpoint:
```bash
curl -X POST -F "file=@malicious.php" http://example.com/uploads/
```

---

### **19. Automated Reporting**
Schedule Nikto scans and generate reports regularly using `cron`:
```bash
crontab -e
```
Add the following entry for a daily scan:
```bash
0 3 * * * /usr/bin/nikto -h http://example.com -o /reports/scan_$(date +\%F).html -Format html
```

---

Here are even **more advanced examples** to push Nikto's capabilities further in real-world, edge-case, or highly targeted use cases.

---

### **1. Combining Nikto with Nmap**
Use Nmap to identify open ports and feed the results to Nikto for scanning.

#### Step 1: Run Nmap to find open ports:
```bash
nmap -p 80,443,8080 -iL targets.txt -oG nmap_output.txt
```

#### Step 2: Extract targets from Nmap output:
```bash
grep open nmap_output.txt | awk '{print $2":"$3}' | sed 's/\/open//' > nikto_targets.txt
```

#### Step 3: Use the extracted targets with Nikto:
```bash
nikto -h nikto_targets.txt
```

---

### **2. Recursive Scanning**
Use Nikto to recursively scan links found during a scan.

1. Enable the `-FollowRedirects` option:
   ```bash
   nikto -h http://example.com -FollowRedirects
   ```

2. Combine with a spider tool like `wget` or `Burp Suite` to identify additional endpoints, then scan those endpoints:
   ```bash
   wget --spider -r -l 2 -o wget.log http://example.com
   grep "http" wget.log | awk '{print $3}' > additional_urls.txt
   nikto -h additional_urls.txt
   ```

---

### **3. Customized Payload Injection**
Run Nikto with custom payloads to test for vulnerabilities like SQL injection, LFI, or XSS.

#### SQL Injection Example:
Create a list of SQL payloads in a text file (`sql_payloads.txt`):
```plaintext
?id=1'
?id=1' OR '1'='1
?id=1 AND 1=1
```

Run Nikto using `sql_payloads.txt`:
```bash
nikto -h http://example.com -mutate 4 -idfile sql_payloads.txt
```

---

### **4. Advanced Tuning for Multi-Vulnerability Scans**
Perform simultaneous scans for **multiple categories** with precise control:
```bash
nikto -h http://example.com -Tuning 0,1,3,4,6 -Plugins headers,cookies -ssl -v
```
This scans for:
- File/CGI issues (`0`),
- Interesting files (`1`),
- XSS (`3`),
- SQL injection (`4`),
- DoS (`6`).

It uses only the `headers` and `cookies` plugins.

---

### **5. Scan Hidden Directories and Files**
Combine Nikto with `gobuster` or `dirb` to discover hidden files or directories before scanning them with Nikto.

#### Step 1: Use Gobuster to discover hidden files:
```bash
gobuster dir -u http://example.com -w /usr/share/wordlists/dirb/common.txt -o gobuster_output.txt
```

#### Step 2: Extract URLs and scan them with Nikto:
```bash
awk '{print $1}' gobuster_output.txt > urls_to_scan.txt
nikto -h urls_to_scan.txt
```

---

### **6. Header Manipulation Attacks**
Nikto can test for vulnerabilities in HTTP headers.

#### Example: Host Header Injection
Run a scan with a malicious `Host` header:
```bash
nikto -h http://example.com -useragent "Host: malicious.com"
```

#### Example: HTTP Verb Tampering
Check for vulnerabilities in uncommon HTTP methods:
```bash
nikto -h http://example.com -method DELETE
```

---

### **7. Advanced Proxy Configurations**
Scan through a proxy with fine-grained control.

#### Proxy with Authentication:
```bash
nikto -h http://example.com -useproxy http://user:password@proxy.example:8080
```

#### Proxychains for Tor:
Set up `proxychains` to route Nikto requests through Tor:
1. Install and configure `proxychains` and `tor`.
2. Run Nikto through `proxychains`:
   ```bash
   proxychains nikto -h http://example.com
   ```

---

### **8. Rate-Limiting Evasion**
Bypass rate-limiting systems with randomized requests:
```bash
nikto -h http://example.com -randomize -pause 15
```

- `-randomize`: Sends requests in a random order.
- `-pause`: Introduces a 15-second delay between requests.

---

### **9. Cross-Site Scripting (XSS) Detection**
Manually inject XSS payloads and use Nikto to automate the detection:
```bash
nikto -h http://example.com/search?q="<script>alert('XSS')</script>"
```

---

### **10. File Upload Vulnerability Testing**
Test for upload vulnerabilities by scanning directories commonly used for uploads:
```bash
nikto -h http://example.com -Cgidirs /uploads,/files,/tmp
```

---

### **11. Customized Headers and Cookies**
Add advanced headers for testing or bypassing protections:
```bash
nikto -h http://example.com -C "Authorization: Bearer TOKEN" -useragent "Custom-Agent"
```

---

### **12. Evading WAFs (Web Application Firewalls)**
Nikto doesn't have built-in WAF bypass techniques but can integrate with tools like `wafw00f` or `Burp Suite`. For example:

#### Step 1: Detect the WAF:
```bash
wafw00f http://example.com
```

#### Step 2: Configure Nikto with headers or delay techniques to bypass:
```bash
nikto -h http://example.com -pause 10 -useragent "Random-Agent"
```

---

### **13. DNS Enumeration and Virtual Hosts**
Enumerate virtual hosts on a server and scan each:
```bash
nmap --script dns-brute -p 80,443 example.com
```

Extract subdomains from the results and feed them to Nikto:
```bash
nikto -h subdomains.txt
```

---

### **14. Custom Exploitation with Nikto Results**
Export Nikto results and use other tools for follow-up exploitation.

#### Save results in JSON:
```bash
nikto -h http://example.com -o results.json -Format json
```

#### Parse JSON for critical findings:
Use Python or other scripts to extract specific issues from the JSON file:
```python
import json

with open('results.json') as f:
    data = json.load(f)
    for item in data['vulnerabilities']:
        print(f"Vulnerability: {item['name']}, URL: {item['url']}")
```

---

### **15. Multi-Layer Automation**
Automate a pipeline that integrates Nikto with other tools like `Nmap`, `Metasploit`, or `Burp Suite`.

Example Bash Script:
```bash
#!/bin/bash

# Step 1: Run Nmap for open ports
nmap -p 80,443 -iL targets.txt -oG nmap_results.txt

# Step 2: Extract live hosts
grep open nmap_results.txt | awk '{print $2}' > live_hosts.txt

# Step 3: Run Nikto
while read host; do
  nikto -h $host -o nikto_results_$host.html -Format html
done < live_hosts.txt
```

---

Here are **even more advanced examples and strategies** for leveraging Nikto in complex and real-world penetration testing scenarios.

---

### **1. Chain Nikto with Advanced Recon Tools**
Combine Nikto with tools like **Amass**, **Subfinder**, or **Nmap** to target all possible attack surfaces.

#### Step 1: Find Subdomains with Amass:
```bash
amass enum -d example.com -o subdomains.txt
```

#### Step 2: Resolve Subdomains with Massdns:
```bash
massdns -r resolvers.txt -t A -o S -w resolved.txt subdomains.txt
```

#### Step 3: Use Nikto on Resolved Domains:
```bash
cat resolved.txt | cut -d " " -f1 > domains.txt
nikto -h domains.txt -o full_scan_results.txt
```

---

### **2. Cross-Protocol Scanning**
Nikto supports multiple protocols like HTTP, HTTPS, and FTP. Use these to target services beyond basic web applications.

#### Example: FTP Banner Grabbing
```bash
nikto -h ftp://example.com
```

#### Example: HTTP on Custom Protocols
Target unusual services running HTTP:
```bash
nikto -h http://example.com -p 5985  # HTTP over WinRM
```

---

### **3. Multi-Port and Protocol Scans**
Scan multiple ports and protocols in a single command:
```bash
nikto -h http://example.com -p 80,443,8080,8443 -ssl
```

---

### **4. Inject Payloads for Manual Verification**
Manually create payloads for SQLi, XSS, or RCE, and automate with Nikto.

#### Example: SQL Injection Payloads
Prepare a file, `sqli_payloads.txt`:
```plaintext
?id=1'
?id=1 AND 1=1
?id=1' UNION SELECT 1,2,3--
```

Run Nikto with the payloads:
```bash
nikto -h http://example.com -mutate 4 -idfile sqli_payloads.txt
```

---

### **5. Analyze Web Application Misconfigurations**
Use Nikto's **plugins** and **tuning** options for specific configuration checks.

#### Example: Misconfigured Headers
```bash
nikto -h http://example.com -Plugins headers,cookies
```

#### Example: Directory Listing Enabled
Check common misconfigured directories:
```bash
nikto -h http://example.com -Cgidirs /images,/backup,/private
```

---

### **6. Use Nikto for API Endpoint Testing**
Test RESTful APIs for misconfigurations or vulnerabilities.

#### Example: API Endpoints with Auth Tokens
```bash
nikto -h http://api.example.com -C "Authorization: Bearer YOUR_API_TOKEN"
```

#### Example: Test Hidden API Endpoints
Feed Nikto with a list of API endpoints:
```bash
nikto -h api_endpoints.txt
```

---

### **7. Target Server-Side Injection Points**
Focus on potential injection points by limiting to specific tests.

#### Example: Command Injection
```bash
nikto -h http://example.com -Tuning 4 -Plugins commands
```

#### Example: Local File Inclusion (LFI)
```bash
nikto -h http://example.com -findonly .php,.inc,.conf
```

---

### **8. Escalate Findings with Exploit Frameworks**
Integrate Nikto's findings with **Metasploit** or **Burp Suite**.

#### Metasploit Integration
1. Save Nikto results as XML:
   ```bash
   nikto -h http://example.com -o results.xml -Format xml
   ```
2. Import into Metasploit:
   ```bash
   msfconsole
   db_import results.xml
   ```

#### Burp Suite Workflow
- Export Nikto findings into a file:
  ```bash
  nikto -h http://example.com -o findings.txt
  ```
- Use the findings to create a custom Burp Intruder payload.

---

### **9. Nikto on Obfuscated/Hidden Services**
Target non-standard web services.

#### Example: Services Running on Non-Standard Ports
```bash
nikto -h http://192.168.1.1 -p 8080,8443
```

#### Example: Scan Services Exposed via SSH Tunneling
```bash
ssh -L 8080:localhost:80 user@remote-server
nikto -h http://127.0.0.1:8080
```

---

### **10. Detect WAF and Bypass Protections**
#### Step 1: Detect WAF with WAFW00F
```bash
wafw00f http://example.com
```

#### Step 2: Evade WAF with Nikto
- Use a custom **User-Agent** string:
  ```bash
  nikto -h http://example.com -useragent "Mozilla/5.0 (Windows NT 10.0; Win64; x64)"
  ```

- Introduce delays and randomize:
  ```bash
  nikto -h http://example.com -pause 10 -randomize
  ```

---

### **11. Automated Reporting Pipeline**
#### Step 1: Schedule Regular Scans
Create a cron job for automated scans:
```bash
crontab -e
```

Add the following:
```bash
0 2 * * * nikto -h http://example.com -o /path/to/reports/scan_$(date +\%F).html -Format html
```

#### Step 2: Send Reports via Email
Use a script to email reports after the scan:
```bash
#!/bin/bash
nikto -h http://example.com -o /reports/scan_$(date +%F).html -Format html
mail -s "Nikto Scan Report" user@example.com < /reports/scan_$(date +%F).html
```

---

### **12. Test Advanced HTTP Methods**
Check for vulnerabilities in non-standard HTTP methods like `TRACE`, `OPTIONS`, or `PUT`.

#### Example: TRACE Method Vulnerability
```bash
nikto -h http://example.com -method TRACE
```

#### Example: Test PUT Method for Arbitrary File Upload
```bash
nikto -h http://example.com -method PUT -upload /path/to/file.txt
```

---

### **13. Detect Old or Deprecated Protocols**
Scan for deprecated SSL/TLS versions:
```bash
nikto -h https://example.com -ssl
```

---

### **14. Blind Testing of Custom Ports**
If you suspect web services on unusual ports:
```bash
nikto -h 192.168.1.1 -p 8081,8444,9090
```

---

### **15. Comprehensive Multi-Step Attack Simulation**
Automate reconnaissance, scanning, and reporting:
```bash
#!/bin/bash

# Step 1: Discover open ports
nmap -p 80,443,8080 -iL targets.txt -oG nmap_output.txt

# Step 2: Extract live hosts
grep open nmap_output.txt | awk '{print $2":"$3}' | sed 's/\/open//' > nikto_targets.txt

# Step 3: Run Nikto for each target
while read target; do
    nikto -h $target -o /reports/nikto_$target.html -Format html
done < nikto_targets.txt
```

---

These examples explore advanced techniques to maximize Nikto’s effectiveness in penetration tests and real-world assessments. Let me know if you want custom examples tailored to a specific attack scenario or environment!
