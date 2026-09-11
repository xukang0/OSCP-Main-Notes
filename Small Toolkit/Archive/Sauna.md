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
Open 10.129.95.180:53 DNS
Open 10.129.95.180:80 HTTP
Open 10.129.95.180:88 LDAP
Open 10.129.95.180:135 RPC
Open 10.129.95.180:139 SMB
Open 10.129.95.180:389 
Open 10.129.95.180:445
Open 10.129.95.180:464
Open 10.129.95.180:593
Open 10.129.95.180:3268
Open 10.129.95.180:3269
Open 10.129.95.180:5985 EvilWinRM
Open 10.129.95.180:9389
Open 10.129.95.180:49667
Open 10.129.95.180:49674
Open 10.129.95.180:49673
Open 10.129.95.180:49676
Open 10.129.95.180:49688
Open 10.129.95.180:49697

53/tcp    open  domain        syn-ack ttl 127 (generic dns response: SERVFAIL)
| fingerprint-strings: 
|   DNS-SD-TCP: 
|     _services
|     _dns-sd
|     _udp
|_    local
80/tcp    open  http          syn-ack ttl 127 Microsoft IIS httpd 10.0
|_http-title: Egotistical Bank :: Home
|_http-server-header: Microsoft-IIS/10.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
88/tcp    open  kerberos-sec  syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2026-09-11 17:45:17Z)
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: EGOTISTICAL-BANK.LOCAL, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds? syn-ack ttl 127
464/tcp   open  kpasswd5?     syn-ack ttl 127
593/tcp   open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
3268/tcp  open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: EGOTISTICAL-BANK.LOCAL, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped    syn-ack ttl 127
5985/tcp  open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
9389/tcp  open  mc-nmf        syn-ack ttl 127 .NET Message Framing
49667/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49673/tcp open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
49674/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49676/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49688/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49697/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC

53/udp    open          domain        (generic dns response: NOTIMP)
123/udp   open          ntp           NTP v3
```

---
## Software Versions

```powershell
OS: Windows 10, Windows Server 2019, Windows Server 2016
OS version: '10.0'
OS release: '1809'
OS build: '17763
```

---
## Discovered Subdomains

DNS domain: EGOTISTICAL-BANK.LOCAL
FQDN: SAUNA.EGOTISTICAL-BANK.LOCAL

---
## Discovered Credentials

fsmith/Thestrokes23
```
Thestrokes23
```

svc_loanmgr
```
Moneymakestheworldgoround!
```

---
## Interesting Files/Paths

---
## Attack Ideas

---
## Steps to User.txt

Since there are no usernames, run kerbrute. 

Discover f.smith and add to Users.txt

f.smith is asrep roastable.

Cracking his hash reveals his creds fsmith/Thestrokes23

netexec sweep shows winrm p3wned!

Login through evilwin-rm

Flag on his desktop

---
## Steps to root.txt

Nothing interesting on whoami /priv

Checking autologon yields password of svc_loanmgr

Login using evilwinrm

Bloodhound tells me dcsync can send me to DC

I run secretsdump, crack it, and pass the hash into admin

---
## User Flag

```

```

## Root Flag

```

```