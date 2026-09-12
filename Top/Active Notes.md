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
Open 10.129.228.253:53 DNS
Open 10.129.228.253:88 Kerb
Open 10.129.228.253:135 RPC
Open 10.129.228.253:139 SMB
Open 10.129.228.253:389 LDAP
Open 10.129.228.253:445
Open 10.129.228.253:464
Open 10.129.228.253:593
Open 10.129.228.253:636
Open 10.129.228.253:1433
Open 10.129.228.253:3269
Open 10.129.228.253:3268
Open 10.129.228.253:5985 WinRM
Open 10.129.228.253:9389
Open 10.129.228.253:49667
Open 10.129.228.253:49673
Open 10.129.228.253:49674
Open 10.129.228.253:49694
Open 10.129.228.253:49704
Open 10.129.228.253:49727

53/tcp    open  domain        syn-ack ttl 127 (generic dns response: SERVFAIL)
88/tcp    open  kerberos-sec  syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2026-09-12 16:23:02Z)
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory 
445/tcp   open  microsoft-ds? syn-ack ttl 127
464/tcp   open  kpasswd5?     syn-ack ttl 127
593/tcp   open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ssl/ldap      syn-ack ttl 127 Microsoft Windows Active Directory 
1433/tcp  open  ms-sql-s      syn-ack ttl 127 Microsoft SQL Server 2019 15.00.2000.00; RTM
| ms-sql-info: 
|   10.129.228.253:1433: 
|     Version: 
|       name: Microsoft SQL Server 2019 RTM
|       number: 15.00.2000.00
|       Product: Microsoft SQL Server 2019
|       Service pack level: RTM
|       Post-SP patches applied: false

|     DNS_Domain_Name: sequel.htb
|     DNS_Computer_Name: dc.sequel.htb

3268/tcp  open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory 
3269/tcp  open  ssl/ldap      syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: sequel.htb, Site: Default-First-Site-Name)
5985/tcp  open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 
9389/tcp  open  mc-nmf        syn-ack ttl 127 .NET Message Framing
49667/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49673/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49674/tcp open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
49694/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49704/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49727/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC


```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

---
## Discovered Credentials

PublicUser : GuestUserCantWrite1

---
## Interesting Files/Paths

---
## Attack Ideas

---
## Steps to User.txt

nmap shows domain name is sequel.htb

PDF File on SMB give creds  

---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```