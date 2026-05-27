[[Exhaustive Ultimate Checklist Template]]
## 1. Initial Enumeration

[[1. Initial Enumeration]]

> [!note]- Initial
>  #### Setup
>   - [ ] [[0000021| [PG Practice] Initial Setup ]]
>   - [ ] [[0000022| [HTB] Initial Setup ]]
>   - [ ] [[0000023| [HTB Seasonal] Initial Setup ]]
>
>  #### NMAP
> - [ ] [[0000001|Full -A Scan]]
> - [ ] [[0000001|UDP Scan]]
> 
> #### Host
> - [ ] [[0000003|Add discovered hosts to /etc/hosts]]

---
## 2. Foothold

> [!note]- General
>  #### General
> - [ ] [[0000004|steghide --extract -sf image.jpg]]
> - [ ] [[0000005|searchsploit all port service versions]]
> - [ ] [[0 Port Number Table|Check Port Number Table]]
> 
>  #### Toolkit
> - [ ] [[0000031|find / -name [filename] 2>/dev/null]] | Search entire system for path of file
> - [ ] [[Root Methods]]
> - [ ] [[4 Shell Upgrade| Shell Upgrade]]
> - [ ] [[Synced OSCP Notes/Small Toolkit/Tools/Hashcat|Hashcat]]
> - [ ] [[Reverse Shell Resources]]

## 2. Service Enumeration

### 🌐 [[80 - WEB | Web]] (80/443)


> [!note]- Web Checklist
> - [ ] [[0000006|Visit site]]
> - [ ] View source
> - [ ] Identify tech/CMS
> - [ ] [[0000008|whatweb]]
> - [ ] [[0000009|Test parameters (?id=1, ?page=) | ?[parameter]=0]]
> - [ ] Analyze error page
> - [ ] [[0000010|curl -i domain]]
>
> #### Brute Force
> - [ ] [[0000011|Feroxbuster Directories brute force (medium)]]
> - [ ] [[0000012|Vhost brute force]]
> - [ ] [[0000013|Feroxbuster File directories sweep]]
>
> #### Vulnerability Testing
> - [ ] [[0000014|LFI (../../../../etc/passwd)]]
> - [ ] [[0000015|SQLi (test' or 1=1;-- -) ]] | [[SQL Injection]]
> - [ ] [[Synced OSCP Notes/Tools/SQLmap|SQLmap]]
> - [ ] [[0000027|URL Webshell]]
> - [ ] [[0000016|Command Injection (;whoami)]]
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
> - [ ] [[Wordpress Scan]]


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

> [!note]- Redis (6379)
> #### Redis 5.0.9
> - [ ] [[6379 Redis]]
>

---
## 4. Privilege Escalation

> [!note]- Priv Esc
>
>  #### LinPEAS
> - [x] Run [[LinWinPEAS]] | [[0000002|parsePEAS-ng]]
> - [x] Run [[Linux Smart Enumeration|LSE.sh]]
> - [x] [[3. Privilege Escalation|HackTricks]]
> - [ ] Review yellow findings
> - [ ] Linux Exploit Suggester
> 
> #### Basic Enumeration
> - [x] whoami
> - [x] id
> - [x] groups
> - [ ] ip a
> - [ ] uname -a
> - [x] env
> 
> #### Advanced Enumeration 
> - [x] Internal ports | [[0000024|ss -tlpn]]
> - [x] Running Processes | [[0000025|ps auxww]]
> - [ ] [[0000026|ls -la /etc/systemd/system/]]
> - [ ] cat /etc/fstab | grep hidepid
> - [ ] enumerate configuration files for passwords
> - [ ] Look through SSH History
> - [ ] Hydra crack
> - [ ] ls 
> 
>  #### SUID / Capabilities
> - [x] [[0000017|find / -perm -4000 2>/dev/null]]
> - [x] [[0000018|getcap -r / 2>/dev/null]]
> - [x] [[GTFOChecker]]
> 
> #### Easy wins
> - [ ] cat /etc/passwd
> - [ ] Try username same as password
> - [x] [[0000032|docker ps]]
> - [ ] ls -la /etc/passwd allowing group modification to root grp
> - [x] [[0000028|mysql --version]]
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
> - [x] [[2375 Docker API|Docker]]
> - [ ] /etc/sudoers.d/ben | ben ALL=(ALL) NOPASSWD:ALL
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
> - [ ] cat /etc/crontab
> - [ ] ls -la /etc/cron* | e2scrub_all , PHP
> - [ ] crontab -l
> - [ ] systemctl list-timers --all
> - [ ] grep -R "" /etc/cron*
> - [ ] [[pspy]]
> 
>  #### Special Permissions
>  - [ ] ls -la /usr/bin/
>
>  #### Writable Content
>- [x] [[0000019|find / -path /proc -prune -o -type d -perm -o+w 2>/dev/null]] | Directories
>- [x] [[0000020|find / -path /proc --prune --o --type f --perm --o+w 2>/dev/null]] | Files
>

> [!note]- Others
>  #### DBMaria
> - [ ] find / -type f -name "*.db" 2>/dev/null
> - [ ]  [[Sqlite| .db]] file found
> - [ ] [[3306 MySQL|MySQL Login Creds Found]]
> 
>  #### Wordpress
> - [ ] cat /srv/http/wp-config.php
> 
>  #### Root 
> - [ ] [[0000030|echo [user] ALL=(ALL) ALL >> /etc/sudoers]]

> [!note]- SUID / Capabilities / Sudo
>  #### FREE WINS SUID
> - [ ] /usr/bin/[[php7.4]]
> - [ ] /usr/bin/find
> - [ ] [[dosbox|/usr/bin/dosbox]]
> 
>  #### FREE WINS SUDO
> - [ ] [[0000026|/bin/systemctl]] | Potential Modification of service in /etc/systemd/system

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
>  - [ ] [[LD_LIBRARY_PATH Hijack]] 
>
>  #### Kernel
>  - [ ] [CVE-2022-0847] Dirtypipe
> 
>  #### Systemctl modifiication
> - [ ] [[0000026|Modifying a service in /etc/systemd/system/]]
> 
>  #### MySQL
> - [ ] [[0000029|ZoneMinder Console v1.29.0 OS-Shell]]


---

## 5. Post Access