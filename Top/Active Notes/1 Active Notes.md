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
53/tcp    open  domain       syn-ack ttl 125 (generic dns response: SERVFAIL)
88/tcp    open  kerberos-sec syn-ack ttl 125 Microsoft Windows Kerberos (server time: 2026-11-06 15:33:51Z)
135/tcp   open  msrpc        syn-ack ttl 125 Microsoft Windows RPC
139/tcp   open  netbios-ssn  syn-ack ttl 125 Microsoft Windows netbios-ssn
389/tcp   open  ldap         syn-ack ttl 125 Microsoft Windows Active Directory LDAP (Domain: secura.yzx, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds syn-ack ttl 125 Windows Server 2016 Standard 14393 microsoft-ds (workgroup: SECURA)
464/tcp   open  kpasswd5?    syn-ack ttl 125
593/tcp   open  ncacn_http   syn-ack ttl 125 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped   syn-ack ttl 125
3268/tcp  open  ldap         syn-ack ttl 125 Microsoft Windows Active Directory LDAP (Domain: secura.yzx, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped   syn-ack ttl 125
5985/tcp  open  http         syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0
5986/tcp  open  ssl/wsmans?  syn-ack ttl 125
9389/tcp  open  mc-nmf       syn-ack ttl 125 .NET Message Framing
49665/tcp open  msrpc        syn-ack ttl 125 Microsoft Windows RPC
49666/tcp open  msrpc        syn-ack ttl 125 Microsoft Windows RPC
49668/tcp open  msrpc        syn-ack ttl 125 Microsoft Windows RPC
49673/tcp open  ncacn_http   syn-ack ttl 125 Microsoft Windows RPC over HTTP 1.0
49674/tcp open  msrpc        syn-ack ttl 125 Microsoft Windows RPC
49675/tcp open  msrpc        syn-ack ttl 125 Microsoft Windows RPC
49703/tcp open  msrpc        syn-ack ttl 125 Microsoft Windows RPC
49746/tcp open  msrpc        syn-ack ttl 125 Microsoft Windows RPC

Host script results:
|_clock-skew: mean: 0s, deviation: 2s, median: -2s
| smb-os-discovery: 
|   OS: Windows Server 2016 Standard 14393 (Windows Server 2016 Standard 6.3)
|   Computer name: dc01
|   NetBIOS computer name: DC01\x00
|   Domain name: secura.yzx
|   Forest name: secura.yzx
|   FQDN: dc01.secura.yzx

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