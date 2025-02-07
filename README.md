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

Let me know if you need more tailored examples or specific guidance!
