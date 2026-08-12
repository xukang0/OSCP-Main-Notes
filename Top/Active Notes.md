[[Active Notes Template]]
## Provided Credentials
---

```

```

```

```

---
## Open Ports

```powershell
53/tcp    open  domain        Simple DNS Plus
80/tcp    open  http          Microsoft IIS httpd 10.0

88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2026-08-12 13:52:09Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: hutch.offsec, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: hutch.offsec, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp  open  mc-nmf        .NET Message Framing
49666/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49673/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49674/tcp open  msrpc         Microsoft Windows RPC
49676/tcp open  msrpc         Microsoft Windows RPC
49692/tcp open  msrpc         Microsoft Windows RPC
50248/tcp open  msrpc         Microsoft Windows RPC


53/udp  open  domain
88/udp  open  kerberos-sec
123/udp open  ntp

```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

---
## Discovered Credentials

fmcsorley
CrabSharkJellyfish192

---
## Interesting Files/Paths

---
## Attack Ideas

---
## Steps to User.txt

[[389 LDAP]] ldapsearch to find creds

use creds to enter Cadaver

Use [[80 WebDAV|Cadaver]] to scan port 80 and access share

Follow [[80 WebDAV]] steps.

---
## Steps to root.txt



---
## User Flag

```

```

## Root Flag

```

```