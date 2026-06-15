[[Active Notes Template]]

[[Active Machine Template]]

| Machine | IP Address | Notes |
| ------- | ---------- | ----- |
|         |            |       |

MACHINE:: Checkpoint
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const machine = page?.MACHINE ?? "NO MACHINE FOUND";

const command = `${machine}`;

dv.paragraph("```bash\n" + command + "\n```");
```
IP::   10.129.189.5
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
KALI IP::  10.10.16.130
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `${KaliIP}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Discovered Web Domain::  10.129.189.5
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `http://${discoveredDomain}/`;

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

```powershell
PORT    STATE SERVICE
53/udp  open  domain
88/udp  open  kerberos-sec
123/udp open  ntp

PORT      STATE SERVICE           VERSION
53/tcp    open  domain            Simple DNS Plus
88/tcp    open  kerberos-sec      Microsoft Windows Kerberos (server time: 2026-06-15 17:34:49Z)
135/tcp   open  msrpc             Microsoft Windows RPC
139/tcp   open  netbios-ssn       Microsoft Windows netbios-ssn
389/tcp   open  ldap              Microsoft Windows Active Directory LDAP (Domain: checkpoint.htb, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http        Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ldapssl?
3268/tcp  open  ldap              Microsoft Windows Active Directory LDAP (Domain: checkpoint.htb, Site: Default-First-Site-Name)
3269/tcp  open  globalcatLDAPssl?
5985/tcp  open  http              Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp  open  mc-nmf            .NET Message Framing
49664/tcp open  msrpc             Microsoft Windows RPC
49668/tcp open  msrpc             Microsoft Windows RPC
49669/tcp open  msrpc             Microsoft Windows RPC
49675/tcp open  msrpc             Microsoft Windows RPC
49676/tcp open  ncacn_http        Microsoft Windows RPC over HTTP 1.0
49686/tcp open  msrpc             Microsoft Windows RPC
49706/tcp open  msrpc             Microsoft Windows RPC
49715/tcp open  msrpc             Microsoft Windows RPC
```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

---
## Discovered Credentials

---
## Interesting Files/Paths

---
## Attack Ideas

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