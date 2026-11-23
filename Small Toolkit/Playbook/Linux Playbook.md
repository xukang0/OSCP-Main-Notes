[[Windows Playbook]]
[[Active Directory Playbook]]

[[0000021| [PEN200] Initial Setup ]]

---

Find out if box is windows or linux
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `ping ${IP}`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```

ttl = 61 > Linux
ttl = 126 > Windows

---
##### `Test Connectivity from TARGET to KALI`
On KALI start listener
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `nc -lvnp 4444`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
On TARGET, ping KALI
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `nc -nv ${KaliIP} 4444`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```

---
# Linux

[[Port Service Enumeration]]

#### Initial access stuck

If SSH open, try name:name of any person you find
[[SQL Injection]]
[[Hydra]]
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `tree -a`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```

Python Detector
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `python3 ~/Desktop/Tools/PythonDetector.py [script]`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```

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
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `sudo -l`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `getcap -r / 2>/dev/null`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `find / -perm -4000 2>/dev/null`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```

GTFOChecker
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `~/Desktop/Tools/GTFOChecker/gtfoChecker`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```

#### Easy wins
cat /etc/passwd
Try username same as password
[[0000032|docker ps]]
Disk Group
ls -la /etc/passwd allowing group modification to root grp
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `mysql --version`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```

#### `Writable Content`
Writeable Directories
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `find / -path /proc -prune -o -type d -perm -o+w 2>/dev/null`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
Writeable Files
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `find / -path /proc -prune -o -type f -perm -o+w 2>/dev/null`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```

#### `Scheduled Tasks`
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `cat /etc/crontab`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
[[incrontab]]
ls -la /etc/cron* | e2scrub_all , PHP
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `crontab -l`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `systemctl list-timers --all`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
grep -R "" /etc/cron*
[[pspy]]
[[proc]]

#### Vulnerability Testing
ls -la /var/www
ls -a ~
.bash_history
interesting files
 
#### PE Vectors (Ruling Out)
 [[2375 Docker API|Docker]]
/etc/sudoers.d/ben | ben ALL=(ALL) NOPASSWD:ALL

#### Priv Checks (Windows)
whoami /priv
whoami /groups

#### Special Permissions
ls -la /usr/bin/


>  #### Others
zip file > John2zip
[[PwnKit]]
Raptor2UC MySQL

>  #### Path Hijacking
>  - [ ] [[Python Library Hijacking]]
>  - [ ] [[LD_LIBRARY_PATH Hijack]] 
>  - [ ] [[Cronjob Path Hijack]]
[[Cronjob Wildcard Hijack]]


>  #### DBMaria
> - [ ] find / -type f -name "*.db" 2>/dev/null
> - [ ]  [[SQLite| .db]] file found
> - [ ] [[3306 MySQL|MySQL Login Creds Found]]
> 
>  #### Wordpress
> - [ ] cat /srv/http/wp-config.php
> 
>  #### Root 
> - [ ] [[0000030|echo [user] ALL=(ALL) ALL >> /etc/sudoers]]

> #### Ports
> - [ ]  [[3000 Grafana| Port 3000 Grafana]]
> - [ ]  [[Node Inspector | Port 9229 Node Inspector]]
> - [ ]  [[10050 Zabbix|Port 10050 Zabbix]]
> 
>  #### Web
> - [ ]  [[Jenkins Priv Esc|Jenkins Internal Server and File Read]]
> 

>
> #### Exiftool
>  - [ ] [[Vulnerable ExifTool DjVu Priv Esc]]

>  #### Kernel
>  - [ ] [CVE-2022-0847] Dirtypipe
> 
>  #### Systemctl modifiication
> - [ ] [[0000026|Modifying a service in /etc/systemd/system/]]
> 
>  #### MySQL
> - [ ] [[0000029|ZoneMinder Console v1.29.0 OS-Shell]]

SUID / Capabilities / Sudo
>  #### FREE WINS SUID
> - [ ] /usr/bin/[[php7.4]]
> - [ ] /usr/bin/find
> - [ ] [[dosbox|/usr/bin/dosbox]]
/usr/bin/[[gcore]]
> 
>  #### FREE WINS SUDO
> - [ ] [[0000026|/bin/systemctl]] | Potential Modification of service in /etc/systemd/system
> - [ ] [[0000039|GTFOBins Systemctl]] 




