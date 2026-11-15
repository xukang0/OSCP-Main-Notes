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
Nmap scan report for 192.168.162.122
22/tcp filtered ssh     no-response

Nmap scan report for 192.168.162.120
22/tcp filtered ssh     no-response
80/tcp filtered http    no-response

Nmap scan report for 192.168.162.121
PORT    STATE    SERVICE     REASON      VERSION
80/tcp  filtered http        no-response
135/tcp filtered msrpc       no-response
139/tcp filtered netbios-ssn no-response

Nmap scan report for 192.168.162.122
22/tcp filtered ssh     no-response

Nmap scan report for 192.168.162.120

PORT   STATE    SERVICE REASON      VERSION
22/tcp filtered ssh     no-response
80/tcp filtered http    no-response

Nmap scan report for WEB02.dmz.medtech.com (192.168.162.121)
PORT    STATE    SERVICE     REASON      VERSION
80/tcp  filtered http        no-response
135/tcp filtered msrpc       no-response
139/tcp filtered netbios-ssn no-response

Nmap scan report for 172.16.162.11
49664/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49665/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49669/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49674/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC

Nmap scan report for 172.16.162.10
49664/tcp open  msrpc      syn-ack ttl 64 Microsoft Windows RPC
49665/tcp open  msrpc      syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc      syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc      syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc      syn-ack ttl 64 Microsoft Windows RPC
49672/tcp open  msrpc      syn-ack ttl 64 Microsoft Windows RPC
58963/tcp open  ncacn_http syn-ack ttl 64 Microsoft Windows RPC over HTTP 1.0
65357/tcp open  msrpc      syn-ack ttl 64 Microsoft Windows RPC

Nmap scan report for 172.16.162.82
5040/tcp  open  unknown syn-ack ttl 64
49664/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49665/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49669/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49670/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49671/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC

Nmap scan report for 172.16.162.13
49664/tcp open  unknown syn-ack ttl 64
49665/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49669/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49674/tcp open  unknown syn-ack ttl 64

Nmap scan report for 172.16.162.12
49664/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49665/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49669/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49670/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC

Nmap scan report for WEB02.dmz.medtech.com (192.168.162.121)
5985/tcp  open  http        syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
5986/tcp  open  ssl/wsmans? syn-ack ttl 125
47001/tcp open  http        syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc       syn-ack ttl 125 Microsoft Windows RPC
49665/tcp open  msrpc       syn-ack ttl 125 Microsoft Windows RPC
49666/tcp open  msrpc       syn-ack ttl 125 Microsoft Windows RPC
49667/tcp open  msrpc       syn-ack ttl 125 Microsoft Windows RPC
49668/tcp open  msrpc       syn-ack ttl 125 Microsoft Windows RPC
49671/tcp open  msrpc       syn-ack ttl 125 Microsoft Windows RPC
49677/tcp open  msrpc       syn-ack ttl 125 Microsoft Windows RPC
49689/tcp open  msrpc       syn-ack ttl 125 Microsoft Windows RPC

Nmap scan report for 172.16.162.83
5040/tcp  open  unknown syn-ack ttl 64
49664/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49665/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49669/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC
49673/tcp open  msrpc   syn-ack ttl 64 Microsoft Windows RPC

Nmap scan report for 192.168.162.122
1194/tcp open  openvpn? syn-ack ttl 61

Nmap scan report for 172.16.162.11
135/tcp   open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 64 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 64
5985/tcp  open  http          syn-ack ttl 64 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
5986/tcp  open  ssl/http      syn-ack ttl 64 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
47001/tcp open  http          syn-ack ttl 64 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
49664/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49674/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC

Nmap scan report for FILES02.medtech.com (172.16.162.11)
135/tcp   open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 64 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 64
5985/tcp  open  http          syn-ack ttl 64 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
5986/tcp  open  ssl/http      syn-ack ttl 64 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49664/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49674/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC

Nmap scan report for DEV04.medtech.com (172.16.162.12)
135/tcp   open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 64 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 64
3389/tcp  open  ms-wbt-server syn-ack ttl 64 Microsoft Terminal Services
5985/tcp  open  http          syn-ack ttl 64 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
5986/tcp  open  ssl/http      syn-ack ttl 64 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49664/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49670/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49676/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC

Nmap scan report for PROD1.medtech.com (172.16.162.13)
135/tcp   open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 64 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 64
5985/tcp  open  http          syn-ack ttl 64 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
5986/tcp  open  ssl/http      syn-ack ttl 64 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49664/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49674/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC

Nmap scan report for CLIENT01.medtech.com (172.16.162.82)
135/tcp   open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 64 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 64
5985/tcp  open  http          syn-ack ttl 64 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
5986/tcp  open  ssl/http      syn-ack ttl 64 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49664/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49670/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49671/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC

Nmap scan report for WEB02.dmz.medtech.com (192.168.162.121)

80/tcp    open  http          syn-ack ttl 125 Microsoft IIS httpd 10.0
135/tcp   open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 125 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 125
5985/tcp  open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
5986/tcp  open  ssl/wsmans?   syn-ack ttl 125
47001/tcp open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49671/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49677/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49683/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC

Nmap scan report for 192.168.162.120
22/tcp open  ssh     syn-ack ttl 61 OpenSSH 8.4p1 Debian 5+deb11u1 (protocol 2.0)
80/tcp open  http    syn-ack ttl 61 WEBrick httpd 1.6.1 (Ruby 2.7.4 (2021-07-07))

Nmap scan report for 172.16.162.14
22/tcp open  ssh     syn-ack ttl 64 OpenSSH 8.4p1 Debian 5+deb11u1 (protocol 2.0)

Nmap scan report for 192.168.162.122
22/tcp   open  ssh      syn-ack ttl 61 OpenSSH 8.9p1 Ubuntu 3 (Ubuntu Linux; protocol 2.0)

Nmap scan report for DC01.medtech.com (172.16.162.10)
53/tcp    open  domain            syn-ack ttl 64 Simple DNS Plus
88/tcp    open  kerberos-sec      syn-ack ttl 64 Microsoft Windows Kerberos (server time: 2026-11-15 03:30:54Z)
135/tcp   open  msrpc             syn-ack ttl 64 Microsoft Windows RPC
139/tcp   open  netbios-ssn       syn-ack ttl 64 Microsoft Windows netbios-ssn
389/tcp   open  ldap              syn-ack ttl 64 Microsoft Windows Active Directory LDAP (Domain: medtech.com, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?     syn-ack ttl 64
464/tcp   open  kpasswd5?         syn-ack ttl 64
3268/tcp  open  ldap              syn-ack ttl 64 Microsoft Windows Active Directory LDAP (Domain: medtech.com, Site: Default-First-Site-Name)
3269/tcp  open  globalcatLDAPssl? syn-ack ttl 64
5985/tcp  open  http              syn-ack ttl 64 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
5986/tcp  open  ssl/http          syn-ack ttl 64 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49664/tcp open  msrpc             syn-ack ttl 64 Microsoft Windows RPC
49665/tcp open  msrpc             syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc             syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc             syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc             syn-ack ttl 64 Microsoft Windows RPC
49672/tcp open  msrpc             syn-ack ttl 64 Microsoft Windows RPC

Nmap scan report for CLIENT02.medtech.com (172.16.162.83)
135/tcp   open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 64 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 64
5985/tcp  open  http          syn-ack ttl 64 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
5986/tcp  open  ssl/http      syn-ack ttl 64 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49664/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49673/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

---
## Discovered Credentials

uid=sa;password=WhileChirpTuesday218

sa/WhileChirpTuesday218 and joe/Flowers1 doesnt seem to work anywhere

Secret  : _SC_SNMPTRAP / service 'SNMPTRAP' with username : MEDTECH\joe
cur/text: Flowers1

Secret  : _SC_SQLTELEMETRY$SQLEXPRESS / service 'SQLTELEMETRY$SQLEXPRESS' with username : NT Service\SQLTELEMETRY$SQLEXPRESS

Secret  : _SC_SSDPSRV / service 'SSDPSRV' with username : MEDTECH\joe
cur/text: Flowers1

Backup      goomba                       6872 Backup Completed. NTLM: 8e9e1516818ce4e54247e71e71b5f436

 Backup	   wario                        6872 Backup Completed. NTLM: fdf36048c1cf88f5630381c5e38feb8e

 Backup	   toad                         6872 Backup Completed. NTLM: 5be63a865b65349851c1f11a067a3068

Backup      daisy                        6872 Backup Completed. NTLM: abf36048c1cf88f5603381c5128feb8e3


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