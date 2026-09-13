Windows AD

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
53/tcp   open  domain        syn-ack ttl 127 (generic dns response: SERVFAIL)
| fingerprint-strings: 
|   DNS-SD-TCP: 
|     _services
|     _dns-sd
|     _udp
|_    local
88/tcp   open  kerberos-sec  syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2026-09-13 12:46:42Z)
135/tcp  open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
389/tcp  open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: BLACKFIELD.local, Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds? syn-ack ttl 127
593/tcp  open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
3268/tcp open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: BLACKFIELD.local, Site: Default-First-Site-Name)
5985/tcp open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)

```

---
## Software Versions

```powershell
|    Domain Information via SMB session for 10.129.229.17    |
[*] Enumerating via unauthenticated SMB session on 445/tcp
[+] Found domain information via SMB
NetBIOS computer name: DC01
NetBIOS domain name: BLACKFIELD
DNS domain: BLACKFIELD.local
FQDN: DC01.BLACKFIELD.local
Derived membership: domain member
Derived domain: BLACKFIELD

OS: Windows 10, Windows Server 2019, Windows Server 2016
OS version: '10.0'
OS release: '1809'
OS build: '17763'

```

---
## Discovered Subdomains

---
## Discovered Credentials

support
```
#00^BlackKnight
```

svc_backup
```
9658d1d1dcd9250115e2205d9f48400d
```

---
## Interesting Files/Paths

SMB Forensic share

---
## Attack Ideas

---
## Steps to User.txt

nmap scan shows domain is blackfield.local

Add it to /etc/hosts

53DNS axfr transfer failed

88Kerberos open, run kerbrute and rid lookup for users

managed to get a good list of users from rid lookup

Attempt to as-rep these list of users

1 hit, audit2020 gives kerberos hash

john cracks the hash and we have creds for 'support:#00^BlackKnight'

Run nxc sweep on these creds, as well as test the password against all users

Password doesnt work for any other users

RPCclient fails

SMBClient anonymous listing shows "profiles$"

Enum4linux-ng gives us OS information and domain information. Windows 10, Windows server 2019 and windows server 2016

SMB profiles$ give us a whole bunch of profile names. Added to user1 file

[[Sanitizing Files]] and getting a clean user1 file

asrep roast it + trying support pw on it. None hit.

Try ldap. ldapsearch negative

Running bloodhound-python and ingesting, discover support has force password change over audit2020

Change creds with rpcclient to audit2020:Retric!

audit2020 has access to forensic share

there is lsass.zip inside

download and unzip and use pypykatz to dump lsass

NT hash for DC01$ and svc_backup

NT hash can be passed for Evil Win RM. 

Enter svc_backup account. Flag on his desktop

svc_backup has priv for SeBackupPrivilege and SeRestorePrivilege

[[SeBackupPrivilege]] ntds.dit and system secretsdump for hash

pass the hash into evilwin-rm

---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```