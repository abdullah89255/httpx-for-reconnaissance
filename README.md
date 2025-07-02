# httpx-for-reconnaissance
Absolutely! Here are **more unique and practical examples** of using `httpx` for reconnaissance, bug bounty, or penetration testing workflows. These go beyond the basic usage and show powerful features:

---

## 🔹 1. **Check for HTTP/HTTPS support**

```bash
cat domains.txt | httpx -ports 80,443 -probe
```

> Shows whether the domain supports HTTP or HTTPS (good for identifying misconfigured servers).

---

## 🔹 2. **Filter only live hosts with specific status codes**

```bash
cat hosts.txt | httpx -sc -status-code -mc 200,403,401
```

> Returns only URLs responding with 200 (OK), 403 (Forbidden), or 401 (Unauthorized).

---

## 🔹 3. **Find titles and detect technologies**

```bash
cat webhosts.txt | httpx -title -tech-detect
```

> Useful for fingerprinting web applications (like WordPress, Nginx, jQuery).

---

## 🔹 4. **Send custom headers (e.g., bypassing 403)**

```bash
cat targets.txt | httpx -H "X-Forwarded-For: 127.0.0.1"
```

> Try bypassing IP-based access control or WAFs.

---

## 🔹 5. **Find subdomain takeovers**

```bash
cat subdomains.txt | httpx -location -title -no-color | grep -Ei "not found|no such|error|doesn't exist"
```

> Helps in identifying potential subdomain takeover vulnerabilities.

---

## 🔹 6. **Run with multiple threads and timeout**

```bash
cat urls.txt | httpx -t 50 -timeout 5 -status-code
```

> Increase speed (50 threads), reduce timeout (5 sec) for faster results on large lists.

---

## 🔹 7. **Extract IP addresses and CDN detection**

```bash
cat domains.txt | httpx -ip -cdn
```

> Shows IPs and whether domains are behind Cloudflare, Akamai, etc.

---

## 🔹 8. **Check for redirect chains**

```bash
cat urls.txt | httpx -follow-redirects -location
```

> Useful for spotting HTTP to HTTPS redirections or login redirect logic.

---

## 🔹 9. **Check for CORS misconfigurations**

```bash
cat targets.txt | httpx -cors
```

> Detect if servers improperly allow cross-origin requests.

---

## 🔹 10. **Check for response content keywords**

```bash
cat urls.txt | httpx -match-string "admin|login|password"
```

> Find endpoints that return specific keywords (good for login pages, admin panels).

---

## 🔹 11. **Filter servers by TLS version**

```bash
cat domains.txt | httpx -tls-grab -tls-probe | grep TLS
```

> Check which TLS versions are supported. Useful in compliance testing.

---

## 🔹 12. **Probe all HTTP ports (not just 80/443)**

```bash
cat ip_list.txt | httpx -ports 8080,8443,8000,3000 -path /admin -status-code
```

> Scan non-standard ports for admin panels or apps.

---

## 🔹 13. **Find WebSockets support**

```bash
cat hosts.txt | httpx -ws
```

> Detects if WebSocket connections are supported.

---

## 🔹 14. **Save output in JSON format**

```bash
cat targets.txt | httpx -json -o output.json
```

> Parseable and useful for automation or feeding into other tools.

---

## 🔹 15. **Check for known vulnerability banners**

```bash
cat urls.txt | httpx -server -tech-detect | grep -iE "Apache/2.2|PHP/5.6|IIS/6"
```



---
Great! Here's a **fresh list of 20+ advanced and unique `httpx` examples** you can use for recon, vulnerability detection, and automation in bug bounty or pentesting workflows.

---

### ⚙️ ADVANCED & UNIQUE `httpx` EXAMPLES

---

### ✅ 1. **Check for open redirect parameters**

```bash
cat urls.txt | httpx -path "/redirect?url=https://evil.com" -status-code -location
```

> Detects open redirect vulnerabilities by observing the final location.

---

### ✅ 2. **Check for large response size (could be sensitive data)**

```bash
cat urls.txt | httpx -cl | awk '$2 > 50000'
```

> Finds responses > 50KB, which might leak debug logs, databases, etc.

---

### ✅ 3. **Print only vulnerable servers with outdated software**

```bash
cat domains.txt | httpx -server -tech-detect | grep -E "Apache/2\.2|OpenSSL/1\.0"
```

> Filter outdated versions of Apache/OpenSSL.

---

### ✅ 4. **Mass scan and screenshot (with `-screenshot`)**

```bash
cat urls.txt | httpx -screenshot -o screenshots.txt
```

> (Use with `headless` support). Captures screenshots of websites.

---

### ✅ 5. **CVE-specific banner detection**

```bash
cat hosts.txt | httpx -title -server | grep -i "tomcat/7"
```

> Find specific vulnerable versions (e.g., Apache Tomcat 7 for CVE-2017-12615).

---

### ✅ 6. **Use POST method instead of GET**

```bash
cat urls.txt | httpx -x POST
```

> Useful for testing how endpoints respond to POST requests.

---

### ✅ 7. **Use HTTP/2 and show protocol**

```bash
cat urls.txt | httpx -http2 -probe -json
```

> Check HTTP/2 support and output in JSON format.

---

### ✅ 8. **Filter for 401 Unauthorized (login pages)**

```bash
cat urls.txt | httpx -status-code -mc 401
```

> Identify endpoints requiring authentication.

---

### ✅ 9. **Check for Virtual Hosts (vhost fuzzing)**

```bash
ffuf -w vhosts.txt -u http://TARGET -H "Host: FUZZ" | tee vhost-results.txt
```

> Combine with `httpx` output to brute-force vhosts.

---

### ✅ 10. **Send request with raw HTTP header file**

```bash
httpx -u https://example.com -rf custom-headers.txt
```

> Use custom raw headers (like cookie, token, etc.)

---

### ✅ 11. **Detect JSON API endpoints**

```bash
cat urls.txt | httpx -match-regex "application/json" -content-type
```

> Filters API endpoints responding with JSON.

---

### ✅ 12. **Check for cloud misconfigurations**

```bash
cat domains.txt | httpx -title -tech-detect | grep -iE "S3|Azure|DigitalOcean"
```

> Check if cloud services leak information (e.g., open buckets).

---

### ✅ 13. **Filter domains with login in title**

```bash
cat urls.txt | httpx -title | grep -i "login"
```

> Useful for identifying authentication portals.

---

### ✅ 14. **Check for PUT method support**

```bash
cat targets.txt | httpx -x PUT -status-code
```

> Some misconfigured servers allow uploading with PUT (e.g., WebDAV).

---

### ✅ 15. **Use proxy with `httpx`**

```bash
cat urls.txt | httpx -proxy http://127.0.0.1:8080
```

> Route traffic through a proxy (e.g., Burp Suite or TOR).

---

### ✅ 16. **Check for HTTP methods allowed**

```bash
cat targets.txt | httpx -method
```

> Detects supported HTTP methods like PUT, DELETE, OPTIONS.

---

### ✅ 17. **Randomize user agents**

```bash
cat urls.txt | httpx -random-agent
```

> Bypass some WAFs or prevent blocking due to signature detection.

---

### ✅ 18. **Check for known CMS**

```bash
cat domains.txt | httpx -tech-detect | grep -Ei "wordpress|drupal|joomla"
```

> Helps prioritize known CMSes for CMS-specific exploits.

---

### ✅ 19. **Scan only IPv6 hosts**

```bash
cat ipv6_hosts.txt | httpx -ip -prefer-ipv6
```

> If you're targeting IPv6 subnets specifically.

---

### ✅ 20. **Check for JWT support in headers**

```bash
cat urls.txt | httpx -H "Authorization: Bearer fake.jwt.token" -status-code
```

> Useful to identify APIs using JWT auth headers.

---

### ✅ 21. **Chain `subfinder` ➝ `httpx` for full subdomain scan**

```bash
subfinder -d example.com -silent | httpx -silent -status-code -title
```

> Automates enumeration + probing.

---

### ✅ 22. **Save output as CSV**

```bash
cat urls.txt | httpx -title -status-code -ip -csv -o report.csv
```

> Clean format for reporting and triage.

---

Let me know if you want examples of using `httpx` inside Bash/Python scripts, or integrating with tools like `nuclei`, `gau`, `waybackurls`, or `hakrawler`.


