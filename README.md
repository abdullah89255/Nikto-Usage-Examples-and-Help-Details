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

These advanced examples should give you the flexibility to tailor Nikto for specific, real-world scenarios. Let me know if you need more insights or assistance!
