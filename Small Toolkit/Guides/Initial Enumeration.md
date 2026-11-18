Add hosts to /etc/hosts 
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `echo "${ip} ${discoveredDomain}" | sudo tee -a /etc/hosts`;

dv.paragraph("```bash\n" + command + "\n```");
```
---
# Port Scanning

### TCP Scan

Full Rustscan TCP Scan
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo rustscan -a ${ip} -b 500 --ulimit 5000 -- -sC -sV -Pn`;

dv.paragraph("```bash\n" + command + "\n```");
```
Rustscan TCP Multiple IPs
```
sudo rustscan -a ip.txt -b 500 --ulimit 5000 -- -sC -sV -Pn --append-output -oN all_hosts.txt
```

Nmap TCP double check
```
sudo nmap -sS -p- -Pn -A -n -T3 -iL ip.txt -oA nmap_scan
```

### UDP Scan
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo nmap -sU -sS -sV --top-ports 20 --max-retries 1 -Pn -oN udp_scan ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Nmap UDP Multiple IPs
```
sudo nmap -iL ip.txt -sU -sS -sV --version-intensity 0 --top-ports 20 --max-retries 1 -T4 -Pn -oN udp_scan
```

After finding open ports, consult [[0 Port Number Table]].

Visit https://speedguide.net/ports.php

#### Grab banner name
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `telnet ${ip} [port]`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### NXC enumeration
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `nxc smb ${ip} [port] -u '' -p '' --shares`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `smbclient -L \\\\${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### LDAP Enumeration
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `nxc ldap ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ldapsearch -x -H ldap://${ip} -s base namingcontexts`;

dv.paragraph("```bash\n" + command + "\n```");
```
---
# Web

[[0000006|Visit site]]
View source
Identify tech/CMS
[[0000008|whatweb]]
[[0000009|Test parameters (?id=1, ?page=) | ?[parameter]=0]]
Analyze error page
[[Nickel|Curl dead end redirects for error msg]]
[[0000010|Curl -i domain]]

#### Brute Force
[[0000011|Feroxbuster Directories brute force (medium)]]
[[0000011|Feroxbuster WebList brute force]]
[[0000012|Vhost brute force]]
[[0000013|Feroxbuster File directories sweep]]
[[0000038|Feroxbuster API discovery]]

#### Vulnerability Testing
[[0000014|LFI (../../../../etc/passwd)]]
[[0000015|SQLi (test' or 1=1;-- -) ]] | [[SQL Injection]]
[[Synced OSCP Notes/Tools/SQLmap|SQLmap]]
[[0000016|Command Injection (;whoami)]]
PHP code inclusion
File upload (if available)
[[Hexedit]]

#### Hidden Content
Check JS files
Check comments
Check backups (.bak, .zip)

#### Contingencies

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
> - [ ] creds search [service]
>
> #### Reset Password (Email)
> - [ ] If invalid email = does not match our records, SQLi (test' or 1=1;-- -)  [[SQL Injection|link]]
>
> #### Admin Dashboards
> - [ ] Search for framework CVEs
> - [ ] Search for dependencies CVEs
> - [ ] File Uploads for PHP arbitrary code execution [[Arbitrary File Upload Vulnerability|link]]

> [!tip]- Others
>  #### .git / git dumper
> - [ ] Run [[GIT dumper]]
> - [ ] Search for creds
> - [ ] Check commit history
> 
> #### Hash Found
> - [ ] SSH as is
> - [ ] [CyberChef](https://cyberchef.org)
> - [ ] [[Hashcat]]
> 
> #### Wordpress Scan
> - [ ] Default creds
> - [ ] [[Wordpress Scan]]

