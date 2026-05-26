## 1. Initial Enumeration

[[1. Initial Enumeration]]

> [!note]- Initial
>  #### Setup
>   - [ ] [[1. Initial Enumeration|Make Box + NMAP Directory ]]
>
>  #### NMAP
> - [ ] [[0000001|Full -A Scan]]
> - [ ] [[0000002|UDP Scan]]
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
> - [ ] whoami
> - [ ] id
> - [ ] groups
> - [ ] ip a
> - [ ] uname -a
> - [ ] env
> 
> #### Advanced Enumeration 
> - [ ] Internal ports | ss -tlpn
> - [ ] Running Processes | ps auxww
> - [ ] cat /etc/fstab | grep hidepid
> - [ ] enumerate configuration files for passwords
> - [ ] Look through SSH History
> - [ ] Hydra crack
> - [ ] ls 
> 
> #### Easy wins
> - [ ] cat /etc/passwd
> - [ ] Try username same as password
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
> - [ ] Docker
> 	- [ ] cat /etc/resolv.conf
> - [ ] /etc/sudoers.d/ben | ben ALL=(ALL) NOPASSWD:ALL
> 
>#### Priv Checks (LINUX)
> - [ ] sudo -l
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
>  #### SUID / Capabilities
> - [ ] [[0000017|find / -perm -4000 2>/dev/null]]
> - [ ] [[0000018|getcap -r / 2>/dev/null]]
> - [ ] [[GTFOChecker]]
> 
>  #### Special Permissions
>  - [ ] ls -la /usr/bin/
>
>  #### Writable Content
>- [ ] [[0000019|find / -path /proc -prune -o -type d -perm -o+w 2>/dev/null]] | Directories
>- [ ] [[0000020|find / -path /proc --prune --o --type f --perm --o+w 2>/dev/null]] | Files
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