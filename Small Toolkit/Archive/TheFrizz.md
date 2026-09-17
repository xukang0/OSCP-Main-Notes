HTB, Active Directory, WriteGPLink, GPO Abuse 

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

f.frizzle	067f746faca44f170c6cd9d7c4bdac6bc342c608687733f80ff784242b0b0c03	/aACFhikmNopqrRTVz2489

f.frizzle
```
Jenni_Luvs_Magic23
```

---
## Interesting Files/Paths

---
## Attack Ideas

There is an authenticated RCE against the login page
Gibbon LMS < v26.0.00 - Authenticated RCE                                         | php/webapps/51903.py

M.SchoolBus User has bloodhound path to domain admin

F.Frizzle > M.SchoolBus is the target

!suBcig@MehTed!R

---
## Steps to User.txt

[[Current Affairs Notes Template]]]

# Steps to User flag

Nmap scan shows clock skew and domain name frizz.htb

Test DNS. Nothing.

Test RPC. Nothing.

Test SMB. Enum4linux-ng says there is no server. Im guessing this is a pivot internal server

Test Kerb. Cannor rid lookup. Nothing

Visit webpage

Page redirects me to frizzdc.frizz.htb so i add to /etc/hosts

On the page, users mentioned are Mike Smith, Fiona Frizzle, and there is a mention of Azure AD. There is php files

Webpage powered by Gibbon v25.0.00

Attempted various path traversal methods all failed

Tried putting Mike Smith and Fiona Frizzle into users and creating various combinations of possible usernames, kerbrute shows F.Frizzle exists.

F.Frizzle :
1. cant be asrep roasted
2. doesnt use same password as username
GibbonLMS has a github page. I realized i can use path traversal to read existing files

https://github.com/ulricvbs/gibbonlms-filewrite_rce

There is a Gibbon CVE unauthenticated RCE for v 25.01 and before.

It works out of the box and i get a webshell.

Try php payload for Rev shell

I try to upload shell.php through webshell and access through traversal. Pentestmonkey doesnt work so try nc64

running systeminfo through webshell tells us this is windows 2022 and x64

works and i am in frizz\w.webservice

inetpub in root folder. ASPX potential.

nothing in autologon

On Gibbon-LMS there is a config.php file with database creds

in C:\xampp\mysql\bin\sql.exe can execute mysql

Gibbonperson table and pull out password salt, password and username

Hashcat salt crack gives creds

nxc -k shows that kerberos authentication works for this set of creds, use kerberos ticket granting to generate a kerberos ticket.

Request a ticket and login with kerberos ticket through ssh to land on f.frizzle desktop for the user flag.

Checking recycle bin, there is a wapt 7z.

Inside wapt conf folder there is a wapt password when decoded by base64

Use nxc sweep to check this pw

use kerberos ticket granting again for M.schoolbus to ssh in

Use WriteGPLink, [[GPO Abuse]] to get root and get flag


---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```