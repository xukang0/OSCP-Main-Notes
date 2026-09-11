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
Open 10.129.228.111:88 Kerberos
Open 10.129.228.111:135 RPC
Open 10.129.228.111:139 SMB
Open 10.129.228.111:389 
Open 10.129.228.111:445
Open 10.129.228.111:464
Open 10.129.228.111:593
Open 10.129.228.111:636
Open 10.129.228.111:3268
Open 10.129.228.111:3269
Open 10.129.228.111:5985
Open 10.129.228.111:9389
Open 10.129.228.111:49667
Open 10.129.228.111:49673
Open 10.129.228.111:49676
Open 10.129.228.111:49674
Open 10.129.228.111:49693
Open 10.129.228.111:49746

53/tcp    open  domain        syn-ack ttl 127 (generic dns response: SERVFAIL)
88/tcp    open  kerberos-sec  syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2026-09-11 17:28:21Z)
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: MEGABANK.LOCAL, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds? syn-ack ttl 127
464/tcp   open  kpasswd5?     syn-ack ttl 127
593/tcp   open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped    syn-ack ttl 127
3268/tcp  open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: MEGABANK.LOCAL, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped    syn-ack ttl 127
5985/tcp  open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 
9389/tcp  open  mc-nmf        syn-ack ttl 127 .NET Message Framing
49667/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49673/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49674/tcp open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
49676/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49693/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49746/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC


```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

---
## Discovered Credentials

username: AAD_987d7f2f57d2
  name: AAD_987d7f2f57d2
  acb: '0x00000210'
  description: Service account for the Synchronization Service with installation identifier 05c97990-7587-4a3d-b312-309adfc172d9 running on computer MONTEVERDE.
'1601':
  username: mhope
  name: Mike Hope
  acb: '0x00000210'
  description: (null)
'2602':
  username: SABatchJobs
  name: SABatchJobs
  acb: '0x00000210'
  description: (null)
'2603':
  username: svc-ata
  name: svc-ata
  acb: '0x00000210'
  description: (null)
'2604':
  username: svc-bexec
  name: svc-bexec
  acb: '0x00000210'
  description: (null)
'2605':
  username: svc-netapp
  name: svc-netapp
  acb: '0x00000210'
  description: (null)
'2613':
  username: dgalanos
  name: Dimitris Galanos
  acb: '0x00000210'
  description: (null)
'2614':
  username: roleary
  name: Ray O'Leary
  acb: '0x00000210'
  description: (null)
'2615':
  username: smorgan
  name: Sally Morgan
  acb: '0x00000210'
  description: (null)

[+] MEGABANK.LOCAL\SABatchJobs:SABatchJobs 

```
SABatchJobs
```

```
4n0therD4y@n0th3r$
```

---
## Interesting Files/Paths

---
## Attack Ideas

---
## Steps to User.txt

enum4linux-ng reveals several users

None can as-rep

Passwording spraying same pw as user gives creds [+] MEGABANK.LOCAL\SABatchJobs:SABatchJobs 

nxc sweep shows SMB access, access to a share called users$

Recursing the share there is an axure.xml in mhope.

Password">4n0therD4y@n0th3r$</S>

nxc sweep reveals [+] MEGABANK.LOCAL\mhope:4n0therD4y@n0th3r$ (Pwn3d!)

evilwinrm sign in for flag at user desktop

---
## Steps to root.txt



---
## User Flag

```

```

## Root Flag

```

```