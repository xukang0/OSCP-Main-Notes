ESC9, ADCS, Active Directory Assumed Breach

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
Open 10.129.44.127:53 DNS
Open 10.129.44.127:88 Kerb
Open 10.129.44.127:135 RPC
Open 10.129.44.127:139 SMB
Open 10.129.44.127:389 LDAP
Open 10.129.44.127:445
Open 10.129.44.127:464
Open 10.129.44.127:593
Open 10.129.44.127:636
Open 10.129.44.127:3268
Open 10.129.44.127:3269
Open 10.129.44.127:5985 WinRM
Open 10.129.44.127:9389
Open 10.129.44.127:49667
Open 10.129.44.127:49688
Open 10.129.44.127:49687
Open 10.129.44.127:49695
Open 10.129.44.127:49724
Open 10.129.44.127:49743

53/tcp    open  domain        syn-ack ttl 127 (generic dns response: SERVFAIL)
88/tcp    open  kerberos-sec  syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2026-09-18 14:22:15Z)
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory 
445/tcp   open  microsoft-ds? syn-ack ttl 127
464/tcp   open  kpasswd5?     syn-ack ttl 127
593/tcp   open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  ssl/ldap      syn-ack ttl 127 Microsoft Windows Active Directory 
3268/tcp  open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory  
| Subject Alternative Name: DNS:DC01.certified.htb, DNS:certified.htb, DNS:CERTIFIED
| Issuer: commonName=certified-DC01-CA/domainComponent=certified
3269/tcp  open  ssl/ldap      syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: certified.htb, Site: Default-First-Site-Name)
| ssl-cert: Subject: 
| Subject Alternative Name: DNS:DC01.certified.htb, DNS:certified.htb, 
5985/tcp  open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0
9389/tcp  open  mc-nmf        syn-ack ttl 127 .NET Message Framing
49667/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49687/tcp open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
49688/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49695/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49724/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49743/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC

```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

FQDN : DC01.certified.htb
domain : certified.htb
CA : certified-DC01-CA


---
## Discovered Credentials

Given

```
judith.mader : judith09
```

---
## Interesting Files/Paths

---
## Attack Ideas

ADCS

---
## Steps to User.txt

nmap scan shows domain name, CA name, FQDN.

53 DNS X
135 RPC X
139 SMB : Nothing in shares

Judith creds in nxc-sweep shows nothing useful

nxc rid brute gives list of users

as-rep roast gives nothing

Test given password on all users

bloodhound-python using judith creds

judith.mader has writeowner over group management

Management group has GenericWrite over management_svc (user)

WriteOwner group to add judith.mader to management group

Management shadow credentials to management_svc for the NT hash

Evil-winrm into management_svc for user flag

---

shadow creds for management_svc to get into ca_operator. Get NT hash for ca_operator. Test with nxc-sweep

Since account is called ca_operator, try [[ADCS]]

certipy-ad shows ESC9 is available. :CertifiedAuthentication" is the vulnerable template

Follow ESC9 and get administrator hash

nxc-sweep shows evil-winrm is open

root flag on admin desktop

---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```