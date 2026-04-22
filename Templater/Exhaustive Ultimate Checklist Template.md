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

[[0 Port Number Table]]

---
## 3. Lateral Movement

> [!note]- Lateral Movement
>  #### Basic Enumeration
> - [ ] /etc/passwd
> - [ ] Check internal local ports | ss -tlpn
> - [ ] Check currently running processes | ps aux
> - [ ] cat /etc/fstab | grep hidepid
> 
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
> #### Vulnerability Testing
> - [ ] ls -la /var/www
> - [ ] ls -a ~
>   - [ ] .bash_history
>   - [ ] interesting files
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
> - [ ] crontab -l
> 
>  #### SUID / Capabilities
> - [ ] find / -perm -4000 2>/dev/null
> - [ ] getcap -r / 2>/dev/null
> 
>  #### LinPEAS
> - [ ] Run LinPEAS
> - [ ] Review yellow findings


---

## 5. Post Access