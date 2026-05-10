## 1. Initial Enumeration

[[1. Initial Enumeration]]
### Nmap
- [x] Quick Scan
- [x] Full Port Scan
- [x] Service Scan
- [x] UDP Scan

### Post
- [x] Add discovered hosts to /etc/hosts

---
## 2. Foothold

> [!note]- General
>  #### General
> - [ ] steghide --extract -sf image.jpg

[[0 Port Number Table]]

## 2. Service Enumeration

### 🌐 Web (80/443)
> [!note]- Web Checklist
> - [x] Visit site
> - [x] View source
> - [x] Identify tech/CMS
> - [ ] Test parameters (?id=1, ?page=) | ?[parameter]=0
> - [ ] Analyze error page
> - [x] curl -i domain
>
> #### Brute Force
> - [x] Feroxbuster brute force (medium)
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
> - [x] Discover software version
> - [x] Research about software
> - [x] Search and Try Default credentials
> - [x] Research CVEs related to version
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
## 3. Lateral Movement

> [!note]- Lateral Movement
>  #### Basic Enumeration
> - [x] env
> - [x] /etc/passwd
> - [x] Check internal local ports | ss -tlpn
> - [x] Check currently running processes | ps aux
> - [x] cat /etc/fstab | grep hidepid
> - [ ] enumerate configuration files for passwords
> 
> - [ ] Look through SSH History

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
> - [x] cat /etc/passwd
> - [x] docker ps
>
> #### Vulnerability Testing
> - [ ] ls -la /var/www
> - [ ] ls -a ~
>   - [ ] .bash_history
>   - [ ] interesting files
>   
> #### PE Vectors (Ruling Out)
> - [x] Docker
> 	- [ ] cat /etc/resolv.conf
> - [x] /etc/sudoers.d/ben | ben ALL=(ALL) NOPASSWD:ALL
> 
>#### Priv Checks (LINUX)
> - [x] sudo -l
> - [x] strings /usr/bin/usage_management
> 
>#### Priv Checks (Windows)
> - [ ] whoami /priv
> - [ ] whoami /groups
>
> #### Scheduled Tasks
> - [ ] cat /etc/crontab
> - [x] crontab -l
> 
>  #### SUID / Capabilities
> - [x] find / -perm -4000 2>/dev/null
> - [x] getcap -r / 2>/dev/null
> 
>  #### Special Permissions
>  - [x] ls -la /usr/bin/
>
>  #### LinPEAS
> - [ ] Run LinPEAS
> - [ ] Review yellow findings


---

## 5. Post Access