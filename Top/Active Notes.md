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
Open 10.129.44.84:21 FTP 
Open 10.129.44.84:53 DNS
Open 10.129.44.84:88 Kerb
Open 10.129.44.84:135 RPC 
Open 10.129.44.84:139 SMB
Open 10.129.44.84:389 LDAP
Open 10.129.44.84:445
Open 10.129.44.84:464
Open 10.129.44.84:593
Open 10.129.44.84:3268 
Open 10.129.44.84:5985 EvilWin-RM
Open 10.129.44.84:9389
Open 10.129.44.84:47001
Open 10.129.44.84:49664
Open 10.129.44.84:49665
Open 10.129.44.84:49666
Open 10.129.44.84:49668
Open 10.129.44.84:49667
Open 10.129.44.84:55415
Open 10.129.44.84:55420
Open 10.129.44.84:55425
Open 10.129.44.84:55434
Open 10.129.44.84:55447

21/tcp    open  ftp           syn-ack ttl 127 Microsoft ftpd
53/tcp    open  domain        syn-ack ttl 127 (generic dns response: SERVFAIL)
88/tcp    open  kerberos-sec  syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2026-09-18 00:28:25Z)
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: administrator.htb, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds? syn-ack ttl 127
464/tcp   open  kpasswd5?     syn-ack ttl 127
593/tcp   open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
3268/tcp  open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: administrator.htb, Site: Default-First-Site-Name)
5985/tcp  open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0     syn-ack ttl 127 .NET Message Framing
47001/tcp open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0
49664/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
55415/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
55420/tcp open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
55425/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
55434/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
55447/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC

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

administrator.htb

NetBIOS computer name: DC
NetBIOS domain name: ADMINISTRATOR
DNS domain: administrator.htb
FQDN: dc.administrator.htb

---
## Discovered Credentials

Olivia : 
```
ichliebedich
```

Backu
```
tekieromucho
```

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