IP::   10.129.34.178

| Machine | IP Address | Notes |
| ------- | ---------- | ----- |
|         |            |       |
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
Discovered Web Domain::   cacti.monitorsfour.htb
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
wonderful1
```

```

```

[{"id":2,"username":"admin",
"email":"admin@monitorsfour.htb",
"password":"56b32eb43e6f15395f6c46c1c9e1cd36",
"role":"super user",
"token":"8024b78f83f102da4f",
"name":"Marcus Higgins",
"position":"System Administrator",
"dob":"1978-04-26",
"start_date":"2021-01-12",
"salary":"320800.00"},

admin:wonderful1
marcus:wonderful1

{"id":5,"
username":"mwatson",
"email":"mwatson@monitorsfour.htb",
"password":"69196959c16b26ef00b77d82cf6eb169",
"role":"user","
token":"0e543210987654321","
name":"Michael Watson",
"position":"Website Administrator",
"dob":"1985-02-15",
"start_date":"2021-05-11",
"salary":"75000.00"},

{"id":6,"
username":"janderson",
"email":"janderson@monitorsfour.htb","
password":"2a22dcf99190c322d974c8df5ba3256b",
"role":"user",
"token":"0e999999999999999",
"name":"Jennifer Anderson
position":"Network Engineer",
"dob":"1990-07-16",
"start_date":"2021-06-20","
salary":"68000.00"},

{"id":7,
"username":"dthompson","
email":"dthompson@monitorsfour.htb","
password":"8d4a7e7fd08555133e056d9aacb1e519","
role":"user",
"token":"0e111111111111111",
"name":"David Thompson","
position":"Database Manager","
dob":"1982-11-23",
"start_date":"2022-09-15","
salary":"83000.00"}]

---
## Software Versions

 whatweb http://monitorsfour.htb/
http://monitorsfour.htb/ [200 OK] 

Bootstrap, Cookies[PHPSESSID], 

Country[RESERVED][ZZ], 

Email[sales@monitorsfour.htb], 

HTTPServer[nginx], IP[10.129.34.120], 

JQuery, PHP[8.3.27], Script, 

Title[MonitorsFour - Networking Solutions], 

X-Powered-By[PHP/8.3.27], X-UA-Compatible[IE=edge], nginx

---




---

Glenn Jones
Nicola Johnson

sales@monitorsfour.htb

## Open Ports
---
PORT     STATE SERVICE VERSION
80/tcp   open  http    nginx
5985/tcp open  http    Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)

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