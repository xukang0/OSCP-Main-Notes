IP::   192.168.232.32

| Machine | IP Address | Notes |
| ------- | ---------- | ----- |
|         |            |       |

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
KALI IP::  192.168.45.232
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
Discovered Web Domain::  192.168.232.32:8338
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

const command = `wget http://${KaliIP}:8888/[file]`;

dv.paragraph("```bash\n" + command + "\n```");
```
## Provided Credentials
---

```

```

```

```

---
## Open Ports

| Port | Service | Notes |
| ---- | ------- | ----- |
|      |         |       |
22/tcp   open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.4 (Ubuntu Linux; protocol 2.0)

|   256 b9:bc:8f:01:3f:85:5d:f9:5c:d9:fb:b6:15:a0:1e:74 (ECDSA)
|_  256 53:d9:7f:3d:22:8a:fd:57:98:fe:6b:1a:4c:ac:79:67 (ED25519)

80/tcp   open  http    Apache httpd 2.4.52 ((Ubuntu))

8338/tcp open  http    Python http.server 3.5 - 3.10
|_http-title: Maltrail
|_http-server-header: Maltrail/0.52
| http-robots.txt: 1 disallowed entry 
|_/


---
## Software Versions


Maltrail/0.52

---
## Discovered Subdomains




---
## Discovered Credentials

```
$y$j9T$d3tgKD.9dkujxWNbbtZuN1$d6Bcu4MbmSGj.8N2VA1J2tLAT0JvE9OeT9anvuxwA33
```

```
$y$j9T$VdNCwN5thdnTPXpr87UrZ/$DOfFXgmuYsSQZ5S9GU5faFj8Z/BPpLMD80aEPFmIxt9
```

| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---
## Attack Angles

PS AUXWW \ GREPROOT
/usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers

/usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal

/usr/sbin/irqbalance --foreground



---
## Steps to User.txt



---
## Steps to root.txt


---

## User Flag

```

```

## Root Flag

```

```