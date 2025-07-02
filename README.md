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

> Find outdated software for possible CVEs.

---

Would you like examples of combining `httpx` with **`subfinder`**, **`nuclei`**, or in **Bash scripts** for full automation?
