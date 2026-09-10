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
Open 10.129.2.155:53
Open 10.129.2.155:88
Open 10.129.2.155:135
Open 10.129.2.155:139
Open 10.129.2.155:389
Open 10.129.2.155:445
Open 10.129.2.155:464
Open 10.129.2.155:593
Open 10.129.2.155:3268
Open 10.129.2.155:5722
Open 10.129.2.155:9389
Open 10.129.2.155:49152
Open 10.129.2.155:49154
Open 10.129.2.155:49155
Open 10.129.2.155:49153
Open 10.129.2.155:49157
Open 10.129.2.155:49158
Open 10.129.2.155:49165
Open 10.129.2.155:49171
Open 10.129.2.155:49173

53/tcp    open  domain        syn-ack ttl 127 Microsoft DNS 6.1.7601 (1DB15D39) (Windows Server 2008 R2 SP1)
| dns-nsid: 
|_  bind.version: Microsoft DNS 6.1.7601 (1DB15D39)
88/tcp    open  kerberos-sec  syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2026-09-10 18:52:52Z)
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: active.htb, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds? syn-ack ttl 127
464/tcp   open  kpasswd5?     syn-ack ttl 127
593/tcp   open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
3268/tcp  open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: active.htb, Site: Default-First-Site-Name)
5722/tcp  open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
9389/tcp  open  mc-nmf        syn-ack ttl 127 .NET Message Framing
49152/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49153/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49154/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49155/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49157/tcp open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
49158/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49165/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49171/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49173/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
Service Info: Host: DC; OS: Windows; CPE: cpe:/o:microsoft:windows_server_2008:r2:sp1, cpe:/o:microsoft:windows

53/udp    open          domain        Microsoft DNS 6.1.7601 (1DB15D39) (Windows Server 2008 R2 SP1)
123/udp   open          ntp           NTP v3

```

---
## Software Versions

```powershell
OS: Windows 7, Windows Server 2008 R2
OS version: '6.1'
OS release: ''
OS build: '7601'

```

---
## Discovered Subdomains

---
## Discovered Credentials

clsid="{3125E937-EB16-4b4c-9934-544FC6D24D26}" User clsid="{DF5F1855-51E5-4d24-8B1A-D9BDE98BA1D1}"  image="2" changed="2018-07-18 20:46:06" uid="{EF57DA28-5F69-4530-A59E-AAB58578219D}

name="active.htb\SVC_TGS"

edBSHOwhZLTjt/QS9FeIcJ83mjWA98gw9guKOhJOdcqh+ZGMeXOsQbCpZ3xUjTLfCuNH8pG5aSVYdYw/NglVmQ

active.htb\SVC_TGS:GPPstillStandingStrong2k18

active.htb\administrator:Ticketmaster1968

---
## Interesting Files/Paths

---
## Attack Ideas

---
## Steps to User.txt

SMBmap shows read access to Replication share

nmap scan shows domain name is active.htb

recursing the replication share, there is a groups.xml which has username and cpassword

gpp-decrypt cpassword and get creds for SVC_TGS

He has access to replication drive, recursing that drive gives access to user.txt

---
## Steps to root.txt

Running GetUserSPNs gives administrator hash

John the ripper cracks the hash

Use psexec to login through SMB with admin creds

---
## User Flag

```

```

## Root Flag

```

```