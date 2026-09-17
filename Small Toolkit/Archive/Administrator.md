HTB , Active Directory, Breach, 

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


[[Current Affairs Notes Template]]

# Steps to User flag

Nmap scan shows domain is administrator.htb. Add to /etc/hosts

Trying olivia creds to login ftp doesnt work

53 DNS dig finds nothing

RID brute using olivia creds yield list of users. Added to list

RPCclient using olivia fails

enum4linux-ng shows me target OS version and FQDN

Nothing interesting from SMB

Using nxc sweep against oliva creds shows win-rm as pwned

EvilwinRM to enter olivia.

Emily is the only other user on the system

Olivia has GenericAll against Michael

Michael has forcechangepassword of Benjamin

Enter Michael first. Michael entered. Use NXC to check his creds. Nothing.

Onto Benjamin Next. Benjamin on nxc-sweep shows he has access to something on FTP

a psafe3 file was found.

Decrypt it with john for master password, start pwsafe software and open password database

Copy emily password and try nxc-sweep. It works

Evilwinrm into emily. It fails

Use runas to get into emily. Success

User flag on emily desktop

Emily is local administrator but not domain administrator

Emily has genericwrite over ethan

Ethan has GetC GetChangesAll dSet over domain

using targetedkerberoast from emily on ethan, we get his creds.

Since Ethan has DCsync over DC, use impackets-secretsdump to dump admin hash

Evilwinrm using pass the hash into administrator

Flag on admin desktop


---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```