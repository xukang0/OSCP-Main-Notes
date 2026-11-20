[[Windows Playbook]]
[[Active Directory Playbook]]

[[0000021| [PEN200] Initial Setup ]]

---

Find out if box is windows or linux
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ping ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
ttl = 61 > Linux
ttl = 126 > Windows

---
# Linux

[[Linux Initial Enumeration]]

#### Initial access stuck

If SSH open, try name:name of any person you find
[[SQL Injection]]
[[Hydra]]
tree -a

#### General Priv Esc Enumeration

##### `Automated Enumeration Tools`
 [[LinWinPEAS]] | [[0000002|parsePEAS-ng]]
 [[Linux Smart Enumeration|LSE.sh]]
[[3. Privilege Escalation|HackTricks]]
Linux Exploit Suggester

##### `Basic Enumeration`
[[0000033|whoami | id | groups | ip a | uname -a | env]]

##### `Advanced Enumeration`
Internal Ports & Running Processes | [[0000024|ss -tlpn && ps auxww]]
 [[0000026|ls -la /etc/systemd/system/]]
cat /etc/fstab | grep hidepid
enumerate configuration files for passwords
Look through SSH History
Hydra crack
ls 

##### `SUID / Capabilities / Sudo`
[[0000017|find / -perm -4000 2>/dev/null]]
[[0000018|getcap -r / 2>/dev/null]]
sudo -l
[[GTFOChecker]]

#### Easy wins
cat /etc/passwd
Try username same as password
[[0000032|docker ps]]
Disk Group
ls -la /etc/passwd allowing group modification to root grp
[[0000028|mysql --version]]
>
> #### Vulnerability Testing
> - [ ] ls -la /var/www
> - [ ] ls -a ~
>   - [ ] .bash_history
>   - [ ] interesting files
>   
> #### PE Vectors (Ruling Out)
> - [ ] [[2375 Docker API|Docker]]
> - [ ] /etc/sudoers.d/ben | ben ALL=(ALL) NOPASSWD:ALL
> 
>#### Priv Checks (Windows)
> - [ ] whoami /priv
> - [ ] whoami /groups
>
> #### Scheduled Tasks
> - [ ] cat /etc/crontab
> - [ ] [[incrontab]]
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
>- [ ] [[0000019|find / -path /proc -prune -o -type d -perm -o+w 2>/dev/null]] | Directories
>- [ ] [[0000020|find / -path /proc --prune --o --type f --perm --o+w 2>/dev/null]] | Files
>

>  #### Others
zip file > John2zip

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
> - [ ] [[0000039|GTFOBins Systemctl]] 

> [!note]- Priv Esc Techniques
> #### Ports
> - [ ]  [[3000 Grafana| Port 3000 Grafana]]
> - [ ]  [[Node Inspector | Port 9229 Node Inspector]]
> - [ ]  [[10050 Zabbix|Port 10050 Zabbix]]
> 
>  #### Web
> - [ ]  [[Jenkins Priv Esc|Jenkins Internal Server and File Read]]
> 
>  #### Path Hijacking
>  - [ ] [[Python Library Hijacking]]
>  - [ ] [[LD_LIBRARY_PATH Hijack]] 
>  - [ ] [[Cronjob Path Hijack]]
>  - [ ] [[Cronjob Wildcard Hijack]]
>
> #### Exiftool
>  - [ ] [[Vulnerable ExifTool DjVu Priv Esc]]
>
> #### Cron
>  - [ ] /etc/cron.d | e2scrub_all , PHP
>
>  #### Kernel
>  - [ ] [CVE-2022-0847] Dirtypipe
> 
>  #### Systemctl modifiication
> - [ ] [[0000026|Modifying a service in /etc/systemd/system/]]
> 
>  #### MySQL
> - [ ] [[0000029|ZoneMinder Console v1.29.0 OS-Shell]]

