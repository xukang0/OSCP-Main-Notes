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
Open 10.129.1.56:22
Open 10.129.1.56:53
Open 10.129.1.56:80
Open 10.129.1.56:88
Open 10.129.1.56:135
Open 10.129.1.56:139
Open 10.129.1.56:389
Open 10.129.1.56:445
Open 10.129.1.56:464
Open 10.129.1.56:593
Open 10.129.1.56:636
Open 10.129.1.56:9389

22/tcp    open  ssh           syn-ack ttl 127 OpenSSH for_Windows_9.5 (protocol 2.0)
53/tcp    open  domain        syn-ack ttl 127 (generic dns response: SERVFAIL)
88/tcp    open  kerberos-sec  syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2026-09-13 16:21:48Z)
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: frizz.htb, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds? syn-ack ttl 127
464/tcp   open  kpasswd5?     syn-ack ttl 127
593/tcp   open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
3268/tcp  open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: frizz.htb, Site: Default-First-Site-Name)
9389/tcp  open  mc-nmf        syn-ack ttl 127 .NET Message Framing
49664/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49670/tcp open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
58081/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
58090/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
|_clock-skew: 6h59m10s

```

---
## Software Versions

```powershell
Webpage powered by Gibbon v25.0.00

OS Name:                   Microsoft Windows Server 2022 Datacenter
OS Version:                10.0.20348 N/A Build 20348
System Type:               x64-based PC
System Type:               x64-based PC

```

---
## Discovered Subdomains

---
## Discovered Credentials

F.Frizzle

$databaseUsername = 'MrGibbonsDB';
$databasePassword = 'MisterGibbs!Parrot!?1';
$databaseName = 'gibbon';

---
## Interesting Files/Paths

---
## Attack Ideas

There is an authenticated RCE against the login page
Gibbon LMS < v26.0.00 - Authenticated RCE                                         | php/webapps/51903.py

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