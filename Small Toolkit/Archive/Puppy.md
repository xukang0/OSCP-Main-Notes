keepass2john snapd

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
Open 10.129.232.75:53 DNS
Open 10.129.232.75:88 Kerb
Open 10.129.232.75:111 RPCbind
Open 10.129.232.75:135 RPC
Open 10.129.232.75:139 SMB
Open 10.129.232.75:389 LDAP
Open 10.129.232.75:445
Open 10.129.232.75:464
Open 10.129.232.75:593
Open 10.129.232.75:2049 NFS
Open 10.129.232.75:3260
Open 10.129.232.75:3268
Open 10.129.232.75:5985
Open 10.129.232.75:9389
Open 10.129.232.75:49664
Open 10.129.232.75:49668
Open 10.129.232.75:49667
Open 10.129.232.75:49676
Open 10.129.232.75:49691
Open 10.129.232.75:62860
Open 10.129.232.75:65507

53/tcp    open  domain        syn-ack ttl 127 (generic dns response: SERVFAIL)
88/tcp    open  kerberos-sec  syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2026-09-19 00:39:45Z)
111/tcp   open  rpcbind       syn-ack ttl 127 2-4 (RPC #100000)
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: PUPPY.HTB, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds? syn-ack ttl 127
464/tcp   open  kpasswd5?     syn-ack ttl 127
593/tcp   open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
2049/tcp  open  nlockmgr      syn-ack ttl 127 1-4 (RPC #100021)
3260/tcp  open  iscsi?        syn-ack ttl 127
3268/tcp  open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory
5985/tcp  open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 
9389/tcp  open  mc-nmf        syn-ack ttl 127 .NET Message Framing
49664/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49676/tcp open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
49691/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
62860/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
65507/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
```

---
## Software Versions

```powershell
OS: Windows 10, Windows Server 2019, Windows Server 2016
OS version: '10.0'
OS release: ''
OS build: '20348'

```

---
## Discovered Subdomains

puppy.htb

NetBIOS computer name: DC
NetBIOS domain name: PUPPY
DNS domain: PUPPY.HTB
FQDN: DC.PUPPY.HTB


---
## Discovered Credentials

levi.james : KingofAkron2025!

jamie.williams : JamieLove2025!

adam.silver : HJKL2025!

ant.edwards : Antman2025!

steve.tucker : Steve2025! X

samuel.blake : ILY2025! X

steph.cooper : ChefSteph2025!

steph.cooper_adm : FivethChipOnItsWay2025

---
## Interesting Files/Paths

---
## Attack Ideas

Dev share

levi.james is a member of HR group which has genericwrite over dev group

Maybe if we enter dev group we can read the dev share

ant.edwards is a member of senior devs group that has GenericAll against Adam.Silver

---

[[Current Affairs Notes Template]]

# Steps to User flag

nmap scan shows domain is puppy.htb

53 DNS dig nothing

111 rpcbind nothing

135 RPCclient nothing

139 SMBmap only default shares. There is a dev share that i have no access to

enum4linux-ng tells us OS version and domain information

RID brute gives me a list of users

As-rep this list gives nothing

levi.james is a member of HR group which has genericwrite over dev group

Maybe if we enter dev group we can read the dev share

GenericWrite > add levi.james as a member of Dev group allows me to read the dev share

Use keepass2john to crack recovery.kdbx file for "liverpool" password

opening this database shows some users and creds

Compare usernames to rid brute results

nxc sweep these

ant.edwards is the only set of creds that work

ant.edwards is a member of senior devs group that has GenericAll against Adam.Silver

Change Adam Silver password and enable his account

adam silver win rm is allowed

user flag on his desktop

## Steps to root.txt

---

3 users on the system : adam.silver , ant.edwards and steph.cooper

dir -force on root directory shows a backups folder, unzipping it shows steph.cooper password

Window Credential Manager for steph.cooper_adm

Evilwinrm to steph.cooper_adm

steph.cooper_adm is a DC.

Flag on administrator desktop


## User Flag

```

```

## Root Flag

```

```