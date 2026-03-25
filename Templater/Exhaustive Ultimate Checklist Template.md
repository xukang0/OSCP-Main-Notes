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