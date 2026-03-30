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
> - [ ] Try default creds
> - [ ] Test parameters (?id=1, ?page=)
>
> #### Brute Force
> - [ ] Directory brute force (common)
> - [ ] Directory brute force (big)
> - [ ] Vhost brute force
>
> #### Vulnerability Testing
> - [ ] LFI (../../../../etc/passwd)
> - [ ] SQLi (' OR 1=1 --)
> - [ ] Command Injection (; whoami)
> - [ ] File upload (if available)
>
> #### Hidden Content
> - [ ] Check JS files
> - [ ] Check comments
> - [ ] Check backups (.bak, .zip)

#### If Found : Admin Page
> [!tip]- Admin Page
> - [ ] Discover software version
> - [ ] Research about software
> - [ ] Search and Try Default credentials
> - [ ] Research CVEs related to version

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

## 4. Privilege Escalation

> [!note]- Basic Enumeration
> - [ ] whoami
> - [ ] id
> - [ ] uname -a

> [!note]- Sudo
> - [ ] sudo -l

> [!note]- Files
> - [ ] ls -la /var/www
> - [ ] ls -a ~
>   - [ ] .bash_history
>   - [ ] interesting files

> [!note]- Scheduled Tasks
> - [ ] cat /etc/crontab
> - [ ] crontab -l

> [!note]- SUID / Capabilities
> - [ ] find / -perm -4000 2>/dev/null
> - [ ] getcap -r / 2>/dev/null

> [!note]- LinPEAS
> - [ ] Run LinPEAS
> - [ ] Review yellow findings
## 3. Privilege Escalation

- [ ] sudo -l
- [ ] ls -la /var/www
- [ ] cat /etc/crontab
- [ ] crontab -l
- [ ] cat /etc/passwd
- [ ] ls -a ~
	- [ ] cat .bash_history
	- [ ] Look at any non-standard file
- [ ] Run LinPEAS
	- [ ] Yellow Text
	- [ ] Unknown SUID binaries or GUID binaries
	- [ ] Interesting Writable Files owned by me
- [ ] whoami /priv
- [ ] whoami /groups
- [ ] Check for cached creds
- [ ] Check PowerShell History
- [ ] Writable Files/Configs/Cron Jobs
- [ ] Capabilities
- [ ] SUID binaries
- [ ] Kernel Exploits

---
## 4. Lateral Movement

[[4. Lateral Movement]]

- [ ] Check internal local ports
- [ ] Check currently running processes
- [ ] /etc/passwd
- [ ] Look through SSH History

## 5. Post Access