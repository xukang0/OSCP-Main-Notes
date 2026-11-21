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
Open 192.168.200.21:53
Open 192.168.200.21:80
Open 192.168.200.21:88
Open 192.168.200.21:135
Open 192.168.200.21:139
Open 192.168.200.21:389
Open 192.168.200.21:445
Open 192.168.200.21:464
Open 192.168.200.21:593
Open 192.168.200.21:636
Open 192.168.200.21:3268
Open 192.168.200.21:3269
Open 192.168.200.21:3389
Open 192.168.200.21:5985
Open 192.168.200.21:9389

53/tcp    open  domain            syn-ack ttl 125 Simple DNS Plus
80/tcp    open  http              syn-ack ttl 125 Microsoft IIS httpd 10.0
88/tcp    open  kerberos-sec      syn-ack ttl 125 Microsoft Windows Kerberos (server time: 2026-11-21 07:52:11Z)
135/tcp   open  msrpc             syn-ack ttl 125 Microsoft Windows RPC
139/tcp   open  netbios-ssn       syn-ack ttl 125 Microsoft Windows netbios-ssn
389/tcp   open  ldap              syn-ack ttl 125 Microsoft Windows Active Directory LDAP (Domain: nagoya-industries.com, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?     syn-ack ttl 125
464/tcp   open  kpasswd5?         syn-ack ttl 125
593/tcp   open  ncacn_http        syn-ack ttl 125 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ldapssl?          syn-ack ttl 125
3268/tcp  open  ldap              syn-ack ttl 125 Microsoft Windows Active Directory LDAP (Domain: nagoya-industries.com, Site: Default-First-Site-Name)
3269/tcp  open  globalcatLDAPssl? syn-ack ttl 125
3389/tcp  open  ms-wbt-server     syn-ack ttl 125 Microsoft Terminal Services
5985/tcp  open  http              syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
9389/tcp  open  mc-nmf            syn-ack ttl 125 .NET Message Framing
49666/tcp open  msrpc             syn-ack ttl 125 Microsoft Windows RPC
49667/tcp open  msrpc             syn-ack ttl 125 Microsoft Windows RPC
49676/tcp open  ncacn_http        syn-ack ttl 125 Microsoft Windows RPC over HTTP 1.0
49678/tcp open  msrpc             syn-ack ttl 125 Microsoft Windows RPC
49681/tcp open  msrpc             syn-ack ttl 125 Microsoft Windows RPC
49691/tcp open  msrpc             syn-ack ttl 125 Microsoft Windows RPC
49698/tcp open  msrpc             syn-ack ttl 125 Microsoft Windows RPC
49717/tcp open  msrpc             syn-ack ttl 125 Microsoft Windows RPC
```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

---
## Discovered Credentials

craig.carr:Spring2023
fiona.clark:Summer2023
andrea.hayes:Nagoya2023

---
## Interesting Files/Paths

---
## Attack Ideas

Add team names to users

---
## Steps to User.txt

RPCclient null login access denied

With nxc smb, we find out domain name is nagoya-industries.com, machine name is NAGOYA. Add to /etc/hosts

Visiting their webpage, nothing special. But there is a list of names of team members. Dirr fuzz the webpage

This box requires cred engineering. So skip and assumed breach

Fiona.clark has read access to smb shares

With her creds dumb list of users with nxc.

There is no pass-pol

Kerberoasting with fiona.clark gives svc_helpdesk and svc_mssql. Only svc_mssql cracks to Service1

using dotpeek on native laptop to inspect ResetPassword.exe downloaded from SMB NETLOGON share, find svc_helpdesk password

  private static string service_username = "svc_helpdesk";
  private static string service_Password = "U299iYRmikYTHDbPbxPoYYfa2j4x4cdg"; Its not crackable.

Run bloodhound scan

Fionaclark has Genericall to : svc_helpdesk , IAIN.WHITE, JOANNA.WOOD, and BETHAN.WEBSTER

All are members of svc_helpdesk. For now try GenericALl to enter SVC_helpdesk

---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```