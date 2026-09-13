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
Open 10.129.228.120:53 DNS
Open 10.129.228.120:80 HTTP
Open 10.129.228.120:88 Kerb
Open 10.129.228.120:135 RPC
Open 10.129.228.120:139 SMB
Open 10.129.228.120:389 LDAP
Open 10.129.228.120:445
Open 10.129.228.120:464
Open 10.129.228.120:593
Open 10.129.228.120:3268
Open 10.129.228.120:5985 WinRM
Open 10.129.228.120:9389
Open 10.129.228.120:49668
Open 10.129.228.120:49673
Open 10.129.228.120:49674
Open 10.129.228.120:49686
Open 10.129.228.120:49694

53/tcp    open  domain        syn-ack ttl 127 (generic dns response: SERVFAIL)
| fingerprint-strings: 
|   DNS-SD-TCP: 
|     _services
|     _dns-sd
|     _udp
|_    local
80/tcp    open  http          syn-ack ttl 127 Apache httpd 2.4.52 ((Win64) OpenSSL/1.1.1m PHP/8.1.1)
| http-methods: 
|   Supported Methods: GET POST OPTIONS HEAD TRACE
|_  Potentially risky methods: TRACE
|_http-title: g0 Aviation
|_http-server-header: Apache/2.4.52 (Win64) OpenSSL/1.1.1m PHP/8.1.1
88/tcp    open  kerberos-sec  syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2026-09-12 20:43:06Z)
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: flight.htb, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds? syn-ack ttl 127
464/tcp   open  kpasswd5?     syn-ack ttl 127
593/tcp   open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
3268/tcp  open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: flight.htb, Site: Default-First-Site-Name)
5985/tcp  open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 
9389/tcp  open  mc-nmf        syn-ack ttl 127 .NET Message Framing
49668/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49673/tcp open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
49674/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49686/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49694/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

FQDN: g0.flight.htb

---
## Discovered Credentials

svc_apache
```
S@Ss!K@*t13
```

S.Moon
```
S@Ss!K@*t13
```

C.Bum
```
Tikkycoll_431012284
```

---
## Interesting Files/Paths

---
## Attack Ideas

Open 10.129.228.120:53 DNS X
Open 10.129.228.120:80 HTTP 
Open 10.129.228.120:88 Kerb
Open 10.129.228.120:135 RPC
Open 10.129.228.120:139 SMB
Open 10.129.228.120:389 LDAP

index.php indicates its a php website

---
## Steps to User.txt

nmap scan shows domain name is flight.htb

url has RFI

Call back to our smb where Responder catches and gives us ntlmv2 hash

Crack it and get creds for svc_apache

nxc sweep shows smb shares "Web" "Users" and "Shared" exists

SMB share Users show user C.Bum exists

rid brute gives list of users

S.Moon seems to use the same password as svc_apache does

S.Moon has smb write access

Use ntlm_theft to put allfiles into smb and trigger responder for ntlmv2 hash

crack for C.Bum creds

C.Bum has access to Shared folder

Put php webshell into school.flight.htb share

Curl the nc64 to get reverse shell as svc_apache

Use Runas to enter C.Bum Desktop to get flag

---
## Steps to root.txt


---
## User Flag

```

```

## Root Flag

```

```