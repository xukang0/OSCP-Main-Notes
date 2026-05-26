## 1. Initial Enumeration

[[1. Initial Enumeration]]

> [!note]- NMAP
> - [x] Full -A Scan
> - [x] UDP Scan

### Post
- [ ] Add discovered hosts to /etc/hosts

---
## 2. Foothold

> [!note]- General
>  #### General
> - [ ] steghide --extract -sf image.jpg
> - [ ] searchsploit all port service versions

[[0 Port Number Table]]

## 2. Service Enumeration

### 🌐 [[80 - WEB | Web]] (80/443)


> [!note]- Web Checklist
> - [x] Visit site
> - [x] View source
> - [ ] Identify tech/CMS
> - [x] whatweb
> - [ ] Test parameters (?id=1, ?page=) | ?[parameter]=0
> - [ ] Analyze error page
> - [x] curl -i domain
>
> #### Brute Force
> - [ ] Feroxbuster brute force (medium)
> - [ ] Vhost brute force
> - [ ] Feroxbuster File directories sweep
>
> #### Vulnerability Testing
> - [ ] LFI (../../../../etc/passwd)
> - [ ] SQLi (test' or 1=1;-- -) [[SQL Injection]]
> - [ ] Command Injection (; whoami)
> - [ ] PHP code inclusion
> - [ ] File upload (if available)
> - [ ] [[Hexedit]]
>
> #### Hidden Content
> - [ ] Check JS files
> - [ ] Check comments
> - [ ] Check backups (.bak, .zip)

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
> - [ ] admin:admin
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
> - [ ] [[Synced OSCP Notes/Small Toolkit/Tools/John The Ripper|John The Ripper]]
> 
> #### Wordpress Scan
> - [ ] Default creds
> - [ ] wpscan


---

### 🌐 Miscellaneous Ports

> [!note]- SNMP (161/162/10161/10162)
> #### Enumeration
> - [ ] snmpbulkwalk [IP]
> - [ ] snmp-check
>

> [!note]- SMB (139/445)
> #### Enumeration
> - [ ] enum4linux [IP]
>


---
## 4. Privilege Escalation

> [!note]- Priv Esc
> #### Basic Enumeration
> - [x] whoami
> - [x] id
> - [x] groups
> - [x] ip a
> - [x] uname -a
> - [x] env
> 
> #### Advanced Enumeration 
> - [x] Internal ports | ss -tlpn
> - [x] Running Processes | ps auxww
> - [x] cat /etc/fstab | grep hidepid
> - [ ] enumerate configuration files for passwords
> - [ ] Look through SSH History
> - [ ] Hydra crack
> - [x] ls /opt | usually empty
> 
> #### Easy wins
> - [x] cat /etc/passwd
> - [x] Try username same as password
> - [x] docker ps
> - [x] ls -la /etc/passwd allowing group modification to root grp
>
> #### Vulnerability Testing
> - [x] ls -la /var/www
> - [ ] ls -a ~
>   - [ ] .bash_history
>   - [ ] interesting files
> 
> #### Password supersearch
> - [ ] grep -Ff grepcredwords.txt -C 2
>   
> #### PE Vectors (Ruling Out)
> - [x] Docker
> 	- [x] cat /etc/resolv.conf
> - [x] /etc/sudoers.d/ben | ben ALL=(ALL) NOPASSWD:ALL
> 
>#### Priv Checks (LINUX)
> - [x] sudo -l
> - [ ] strings /usr/bin/usage_management
> 
>#### Priv Checks (Windows)
> - [ ] whoami /priv
> - [ ] whoami /groups
>
> #### Scheduled Tasks
> - [x] cat /etc/crontab
> - [x] ls -la /etc/cron* | e2scrub_all , PHP
> - [x] crontab -l
> - [x] systemctl list-timers --all
> - [x] grep -R "" /etc/cron*
> - [ ] [[pspy]]
> 
>  #### SUID / Capabilities
> - [x] find / -perm -4000 2>/dev/null
> - [x] getcap -r / 2>/dev/null
> - [x] [[GTFOChecker]]
> 
>  #### Special Permissions
>  - [x] ls -la /usr/bin/
>
>  #### Writable Content
>- [x] find / -path /proc -prune -o -type d -perm -o+w 2>/dev/null | Directories
>- [x] find / -path /proc --prune --o --type f --perm --o+w 2>/dev/null | Files
>
>  #### LinPEAS
> - [ ] Run [[LinWinPEAS]]
> - [ ] Run [[Linux Smart Enumeration|LSE.sh]]
> - [ ] [[3. Privilege Escalation|HackTricks]]
> - [ ] Review yellow findings
> - [ ] Linux Exploit Suggester
> 

> [!note]- Database
>  #### DBMaria
> - [ ] find / -type f -name "*.db" 2>/dev/null

> [!note]- SUID / Capabilities
>  #### FREE WINS SUID
> - [ ] /usr/bin/[[php7.4]]
> - [ ] /usr/bin/find

> [!note]- Priv Esc Techniques
> #### Ports
> - [ ]  [[Node Inspector | Port 9229 Node Inspector]]
> 
>  #### Python
>  - [ ] [[Python Library Hijacking]]
>
> #### Exiftool
>  - [ ] [[Vulnerable ExifTool DjVu Priv Esc]]
>
> #### Cron
>  - [ ] /etc/cron.d | e2scrub_all , PHP
>
>  #### Kernel
>  - [ ] [CVE-2022-0847] Dirtypipe


---

## 5. Post Access