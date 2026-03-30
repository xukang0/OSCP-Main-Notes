## 1. Initial Enumeration

[[1. Initial Enumeration]]
### Nmap
- [ ] Quick Scan
- [ ] Full Port Scan
- [ ] Service Scan
- [ ] UDP Scan

### Post
- [ ] Add discovered hosts to /etc/hosts

---
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
## 3. Lateral Movement

> [!note]- Lateral Movement
> - [ ] Check internal local ports
> - [ ] Check currently running processes
> - [ ] /etc/passwd
> - [ ] Look through SSH History

---
## 4. Privilege Escalation

> [!note]- Priv Esc
> #### Basic Enumeration
> - [ ] whoami
> - [ ] id
> - [ ] uname -a
> 
> #### Easy wins
> - [ ] cat /etc/passwd
> 
> #### Sudo
> - [ ] sudo -l
>
> #### Vulnerability Testing
> - [ ] ls -la /var/www
> - [ ] ls -a ~
>   - [ ] .bash_history
>   - [ ] interesting files
>   
>#### Priv Checks
> - [ ] sudo -l
> - [ ] whoami /priv
> - [ ] whoami /groups
>
> #### Scheduled Tasks
> - [ ] cat /etc/crontab
> - [ ] crontab -l
> 
>  #### SUID / Capabilities
> - [ ] find / -perm -4000 2>/dev/null
> - [ ] getcap -r / 2>/dev/null
> 
>  #### LinPEAS
> - [ ] Run LinPEAS
> - [ ] Review yellow findings



## 3. Privilege Escalation



- [ ] ls -a ~
	- [ ] cat .bash_history
	- [ ] Look at any non-standard file
- [ ] Run LinPEAS
	- [ ] Yellow Text
	- [ ] Unknown SUID binaries or GUID binaries
	- [ ] Interesting Writable Files owned by me
- [ ] Check for cached creds
- [ ] Check PowerShell History
- [ ] Writable Files/Configs/Cron Jobs
- [ ] Capabilities
- [ ] SUID binaries
- [ ] Kernel Exploits

---

## 5. Post Access