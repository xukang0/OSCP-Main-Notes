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
Open 10.129.227.113:53 DNS
Open 10.129.227.113:88 Kerbe
Open 10.129.227.113:135 RPC
Open 10.129.227.113:139 SMB
Open 10.129.227.113:389 LDAP
Open 10.129.227.113:445 
Open 10.129.227.113:464
Open 10.129.227.113:593
Open 10.129.227.113:636
Open 10.129.227.113:3268
Open 10.129.227.113:3269
Open 10.129.227.113:5986 WinRM
Open 10.129.227.113:9389
Open 10.129.227.113:49667
Open 10.129.227.113:49676
Open 10.129.227.113:49675
Open 10.129.227.113:49697

53/tcp    open  domain        syn-ack 
88/tcp    open  kerberos-sec  syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2026-09-12 13:24:13Z)
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: timelapse.htb, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds? syn-ack ttl 127
464/tcp   open  kpasswd5?     syn-ack ttl 127
593/tcp   open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped    syn-ack ttl 127
3268/tcp  open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: timelapse.htb, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped    syn-ack ttl 127
5986/tcp  open  ssl/wsmans?   syn-ack  commonName=dc01.timelapse.htb
| Issuer: commonName=dc01.timelapse.htb

9389/tcp  open  mc-nmf        syn-ack ttl 127 .NET Message Framing
49667/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49675/tcp open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
49676/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49697/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

FQDN: dc01.timelapse.htb

---
## Discovered Credentials

winrm_backup : supremelegacy

legacyy_dev_auth : thuglegacy

svc_deploy : E3R$Q62^12p7PLlC%KWaxuaV

administrator:P3+Z;]2L1-+T@5Z7VJ2C+l$0

---
## Discovered Users


thecybergeek
payl0ad
legacyy
sinfulz
babywyrm
DB01
WEB01
DEV01
LAPS_Readers
Development
HelpDesk
svc_deploy


---



## Interesting Files/Paths

---
## Attack Ideas

---
## Steps to User.txt

Enum4linux-ng shows FQDN: dc01.timelapse.htb

Inside smb share there is a winbackup.zip that needs john 

Password to zip found and unzip to find a encrypted pfx file

John to crack

rid brute gives me list of usernames

running nxc sweep with supremelegacy and thuglegacy shows me guest has smb access

[[pfx]]

To pass into winRM and land on legacyy desktop for flag

---
## Steps to root.txt

Checking Powershell history gives creds to svc_deploy

member of LAPS reader

HackTricks shows dump password

nxc ldap 10.129.227.113 -u 'svc_deploy' -p 'E3R$Q62^12p7PLlC%KWaxuaV' --kdcHost 10.129.227.113 -M laps dumps admin password

evilwinrm into admin for flag

flag not in admin user

net group 'Domain Admins' to see who the other admins are

There is only 1 user that exist on the computer which is TRX

flag is on TRX Desktop

---
## User Flag

```

```

## Root Flag

```

```