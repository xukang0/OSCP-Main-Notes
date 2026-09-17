ADCS, ESC4, Active Directory

[[Active Notes Template]]
## Provided Credentials
---

```
rose : KxEPkKe6R8su
```

```

```

---
## Open Ports

```powershell
Discovered open port 445/tcp on 10.129.232.128
Discovered open port 139/tcp on 10.129.232.128 SMB
Discovered open port 49691/tcp on 10.129.232.128
Discovered open port 53/tcp on 10.129.232.128 DNS
Discovered open port 636/tcp on 10.129.232.128 LDAP
Discovered open port 135/tcp on 10.129.232.128 RPC
Discovered open port 389/tcp on 10.129.232.128
Discovered open port 49664/tcp on 10.129.232.128
Discovered open port 49690/tcp on 10.129.232.128
Discovered open port 49706/tcp on 10.129.232.128
Discovered open port 9389/tcp on 10.129.232.128
Discovered open port 88/tcp on 10.129.232.128
Discovered open port 49689/tcp on 10.129.232.128
Discovered open port 49667/tcp on 10.129.232.128
Discovered open port 1433/tcp on 10.129.232.128 SQL
Discovered open port 47001/tcp on 10.129.232.128
Discovered open port 49665/tcp on 10.129.232.128
Discovered open port 49730/tcp on 10.129.232.128
Discovered open port 49666/tcp on 10.129.232.128
Discovered open port 3269/tcp on 10.129.232.128
Discovered open port 49720/tcp on 10.129.232.128
Discovered open port 3268/tcp on 10.129.232.128
Discovered open port 5985/tcp on 10.129.232.128 evilwin-rm
Discovered open port 464/tcp on 10.129.232.128
Discovered open port 593/tcp on 10.129.232.128


PORT      STATE SERVICE       REASON          VERSION
53/tcp    open  domain        syn-ack ttl 127 (generic dns response: SERVFAIL)

88/tcp    open  kerberos-sec  syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2026-09-17 19:31:27Z)
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory 
| Subject Alternative Name: DNS:DC01.sequel.htb, DNS:sequel.htb, DNS:SEQUEL
| Issuer: commonName=sequel-DC01-CA/domainComponent=sequel
|_ssl-date: 2026-09-17T19:33:12+00:00; -6h56m53s from scanner time.
445/tcp   open  microsoft-ds? syn-ack ttl 127
464/tcp   open  kpasswd5?     syn-ack ttl 127
593/tcp   open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ssl/ldap      syn-ack ttl 127 Microsoft Windows Active Directory 
1433/tcp  open  ms-sql-s      syn-ack ttl 127 Microsoft SQL Server 2019 
|       name: Microsoft SQL Server 2019 RTM
|       number: 15.00.2000.00
|       Product: Microsoft SQL Server 2019
|       Service pack level: RTM
|       Post-SP patches applied: false
|     Target_Name: SEQUEL
|     NetBIOS_Domain_Name: SEQUEL
|     NetBIOS_Computer_Name: DC01
|     DNS_Domain_Name: sequel.htb
|     DNS_Computer_Name: DC01.sequel.htb
|     DNS_Tree_Name: sequel.htb
|_    Product_Version: 10.0.17763
3268/tcp  open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory 
3269/tcp  open  ssl/ldap      syn-ack ttl 127 Microsoft Windows Active Directory
| Subject Alternative Name: DNS:DC01.sequel.htb, DNS:sequel.htb, DNS:SEQUEL
5985/tcp  open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 
9389/tcp  open  mc-nmf        syn-ack ttl 127 .NET Message Framing
47001/tcp open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0
49664/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49689/tcp open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
49690/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49691/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49706/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49720/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49730/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC

```

---
## Software Versions

```powershell
OS: Windows 10, Windows Server 2019, Windows Server 2016
OS version: '10.0'
OS release: '1809'
OS build: '17763'
```

---
## Discovered Subdomains

DNS domain: sequel.htb
FQDN: DC01.sequel.htb


---
## Discovered Credentials

 username: michael
  username: ryan
  username: oscar
  username: sql_svc
  username: rose
  username: ca_svc
  username: Administrator
  username: Guest
  username: krbtgt

  
Angela,Martin,angela@sequel.htb,angela,0fwz7Q4mSpurIt99
Oscar,Martinez,oscar@sequel.htb,oscar,86LxLBMgEWaKUnBG
Kevin,Malone,kevin@sequel.htb,kevin,Md9Wlq1E5bZnVDVo
NULL,sa@sequel.htb,sa,MSSQLP@ssw0rd!




---
## Interesting Files/Paths

---
## Attack Ideas

ADCS 

---
## Steps to User.txt


[[Current Affairs Notes Template]]

# Steps to User flag

test nxc-sweep on given creds

nmap share shows domain name is sequel.htb

rose has share read access on share "Users" and "Accounting Department"

dig dns finds nothing

RPCclient cant connect

Enum4linux-ng finds list of users, OS information and FQDN

Nothing in mssql

2 xlsx files downloaded from accounting department share. They are zip files.

angela : 0fwz7Q4mSpurIt99 {wrong}
oscar : 86LxLBMgEWaKUnBG {correct}
kevin : Md9Wlq1E5bZnVDVo {wrong}
sa : MSSQLP@ssw0rd!

The sa creds allow commands to be run through mssql for access to sequel\sql_svc shell

The only other user on system is ryan

There is a random password located in sql2019 in root folder

Try to spray it with nxc-sweep

This password works for ryan

I can evilwin-rm into ryan shell. User flag on his desktop

---

ADCS shows that it is vulnerability to ESC4.

Follow ESC4 guide and get administrator hash

nxc-sweep shows evilwinrm is possible

get onto admin desktop and get his flag


---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```