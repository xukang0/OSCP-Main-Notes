## 1. Initial Enumeration

[[1. Initial Enumeration]]
### Nmap
- [x] Quick Scan
- [x] Full Port Scan
- [x] Service Scan
- [x] UDP Scan

### Post
- [ ] Add discovered hosts to /etc/hosts

---
## 2. Foothold

> [!note]- General
>  #### General
> - [ ] steghide --extract -sf image.jpg
> - [x] searchsploit all port service versions

[[0 Port Number Table]]

## 2. Service Enumeration

### 🌐 Web (80/443)
> [!note]- Web Checklist
> - [x] Visit site
> - [ ] View source
> - [x] Identify tech/CMS
> - [x] whatweb
> - [ ] Test parameters (?id=1, ?page=) | ?[parameter]=0
> - [ ] Analyze error page
> - [x] curl -i domain
>
> #### Brute Force
> - [x] Feroxbuster brute force (medium)
> - [ ] Vhost brute force
> - [x] Feroxbuster File directories sweep
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

#### If Found: .Random Hash
> [!tip]- Try
> - [ ] SSH as is
> - [ ] CyberChef
> - [ ] Hashcat

#### If Found: Wordpress [[Wordpress Scan]]
> [!tip]- Wordpress
> - [ ] Default creds
> - [ ] wpscan


---

### 🌐 SNMP (161/162/10161/10162)
> [!note]- SNMP Checklist
> #### Enumeration
> - [ ] snmpbulkwalk [IP]
> - [ ] snmp-check
>


---

### 🌐 SMB (139/445)
> [!note]- SMB Checklist
> #### Enumeration
> - [ ] enum4linux [IP]
>


---
## 3. Lateral Movement

> [!note]- Lateral Movement
>  #### Basic Enumeration
> - [x] env
> - [x] /etc/passwd
> - [x] Check internal local ports | ss -tlpn
> - [x] Check currently running processes | ps auxww
> - [ ] cat /etc/fstab | grep hidepid
> - [ ] enumerate configuration files for passwords
> 
> - [ ] Look through SSH History
> 
> - [ ] Try username same as password
> - [ ] Hydra crack







---
## 4. Privilege Escalation

> [!note]- Priv Esc
> #### Basic Enumeration
> - [x] whoami
> - [x] id
> - [x] groups
> - [x] ip a
> - [x] uname -a
> 
> #### Easy wins
> - [ ] cat /etc/passwd
> - [ ] docker ps
> - [ ] ls -la /etc/passwd allowing group modification to root grp
>
> #### Vulnerability Testing
> - [ ] ls -la /var/www
> - [ ] ls -a ~
>   - [ ] .bash_history
>   - [ ] interesting files
> 
> #### Password supersearch
> - [ ] grep -Ff grepcredwords.txt -C 2
>   
> #### PE Vectors (Ruling Out)
> - [x] Docker
> 	- [ ] cat /etc/resolv.conf
> - [ ] /etc/sudoers.d/ben | ben ALL=(ALL) NOPASSWD:ALL
> 
>#### Priv Checks (LINUX)
> - [ ] sudo -l
> - [x] strings /usr/bin/usage_management
> 
>#### Priv Checks (Windows)
> - [ ] whoami /priv
> - [ ] whoami /groups
>
> #### Scheduled Tasks
> - [ ] cat /etc/crontab
> - [ ] crontab -l
> 
>  #### SUID / Capabilities
> - [x] find / -perm -4000 2>/dev/null
> - [x] getcap -r / 2>/dev/null
> 
>  #### Special Permissions
>  - [ ] ls -la /usr/bin/
>
>  #### Python
>  - [ ] [[Python Library Hijacking]]
>
>  #### LinPEAS
> - [ ] Run [[LinWinPEAS]]
> - [ ] Review yellow findings
> - [ ] Linux Exploit Suggester


---

## 5. Post Access