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
──(kali㉿kali)-[~/…/PEN200/Feast/MS01/nmap]
└─$ cat all_hosts.txt 
# Nmap 7.991 scan initiated Wed Nov 18 11:14:39 2026 as: /usr/lib/nmap/nmap -vvv -p 47001,49664,49665,49666,49667,49669,49674,49675,49676,49687,49711,49784 -4 -sC -sV -Pn --append-output -oN all_hosts.txt 192.168.245.169
Nmap scan report for 192.168.245.169
Host is up, received user-set (0.038s latency).
Scanned at 2026-11-18 11:14:39 EST for 57s

PORT      STATE SERVICE    REASON          VERSION
47001/tcp open  http       syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
49664/tcp open  msrpc      syn-ack ttl 125 Microsoft Windows RPC
49665/tcp open  msrpc      syn-ack ttl 125 Microsoft Windows RPC
49666/tcp open  msrpc      syn-ack ttl 125 Microsoft Windows RPC
49667/tcp open  msrpc      syn-ack ttl 125 Microsoft Windows RPC
49669/tcp open  msrpc      syn-ack ttl 125 Microsoft Windows RPC
49674/tcp open  msrpc      syn-ack ttl 125 Microsoft Windows RPC
49675/tcp open  ncacn_http syn-ack ttl 125 Microsoft Windows RPC over HTTP 1.0
49676/tcp open  msrpc      syn-ack ttl 125 Microsoft Windows RPC
49687/tcp open  msrpc      syn-ack ttl 125 Microsoft Windows RPC
49711/tcp open  msrpc      syn-ack ttl 125 Microsoft Windows RPC
49784/tcp open  msrpc      syn-ack ttl 125 Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Read data files from: /usr/share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Wed Nov 18 11:15:36 2026 -- 1 IP address (1 host up) scanned in 57.27 seconds
# Nmap 7.991 scan initiated Wed Nov 18 11:15:36 2026 as: /usr/lib/nmap/nmap -vvv -p 47001,49664,49666,49665,49667,49668,49670,49673 -4 -sC -sV -Pn --append-output -oN all_hosts.txt 192.168.245.171
# Nmap 7.991 scan initiated Wed Nov 18 11:16:53 2026 as: /usr/lib/nmap/nmap -vvv -p 53,88,135,139,389,445,464,593,636,3268,3269,3389,5985,5986,9389,47001,49664,49665,49666,49667,49669,49674,49675,49676,49687,49711,49784 -4 -sC -sV -Pn --append-output -oN all_hosts.txt 192.168.245.169
Nmap scan report for 192.168.245.169
Host is up, received user-set (0.040s latency).
Scanned at 2026-11-18 11:16:53 EST for 74s

PORT      STATE SERVICE       REASON          VERSION
53/tcp    open  domain        syn-ack ttl 125 Simple DNS Plus
88/tcp    open  kerberos-sec  syn-ack ttl 125 Microsoft Windows Kerberos (server time: 2026-11-18 16:16:59Z)
135/tcp   open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 125 Microsoft Windows netbios-ssn
389/tcp   open  ldap          syn-ack ttl 125 Microsoft Windows Active Directory LDAP (Domain: feast.com, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds? syn-ack ttl 125
464/tcp   open  kpasswd5?     syn-ack ttl 125
593/tcp   open  ncacn_http    syn-ack ttl 125 Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped    syn-ack ttl 125
3268/tcp  open  ldap          syn-ack ttl 125 Microsoft Windows Active Directory LDAP (Domain: feast.com, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped    syn-ack ttl 125
3389/tcp  open  ms-wbt-server syn-ack ttl 125 Microsoft Terminal Services
|_ssl-date: 2026-11-18T16:18:05+00:00; -1s from scanner time.
| ssl-cert: Subject: commonName=DC01.feast.com
| Issuer: commonName=DC01.feast.com
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-11-17T16:03:15
| Not valid after:  2027-05-19T16:03:15
| MD5:     4ac3 ce93 aca4 71c6 637d 35fe b552 d847
| SHA-1:   687f feb0 885b 7384 be2b 65c5 d295 75fd 7c37 d890
| SHA-256: 520a 7191 470a e091 db4f 733b 3223 988b dab6 f797 8a69 950d 0680 b1f5 5497 05ef
| -----BEGIN CERTIFICATE-----
| MIIC4DCCAcigAwIBAgIQFcdQZis/6LpJQsym1iaBxjANBgkqhkiG9w0BAQsFADAZ
| MRcwFQYDVQQDEw5EQzAxLmZlYXN0LmNvbTAeFw0yNjExMTcxNjAzMTVaFw0yNzA1
| MTkxNjAzMTVaMBkxFzAVBgNVBAMTDkRDMDEuZmVhc3QuY29tMIIBIjANBgkqhkiG
| 9w0BAQEFAAOCAQ8AMIIBCgKCAQEA1OmADt8duuNRtPni26Xwqv61QGcIix44HybM
| gf0gielcJWG43Ixg3FZkVGtTipLx4xtMVWyeNd6+6SGmxeeDhYwX54hf38APjmLK
| t5rx4ZF9MSv3SoOpunjvUr0+VFon0UVV2lxSFpuDSlrYRAGFRZaR4yNMZkTKYKlR
| gg091WwPCIBYtnYS3N2cpy7sXQtNmcdZ29qVwynIjBXgeURNIHtBp4R9aBhN7oBM
| KEEWDcM82eXdasEUofiZPjZ4IIiGKrlgTCJ7U3Yfe3jX0Kvy+WRMfDGxfbPqbqB/
| 1Xykwf9c29a26bF5swBXaBImuH7yu1n/ADnLSpZG4EWUW4H4qQIDAQABoyQwIjAT
| BgNVHSUEDDAKBggrBgEFBQcDATALBgNVHQ8EBAMCBDAwDQYJKoZIhvcNAQELBQAD
| ggEBAF7+f1FxlYK2AyMNNva/3mdyrVcDqiPPawdefx1gesOsIcKFAA0hpXwmwMzO
| 9lfu4DoAptQGrHccrcD7snFCBLXCEwn7HzccfuDZ4KtPL87e7/UDMuE3pEvDqc2U
| eoYgV/j+aHFF+io3RB1HgvsjGCUIZg+8yD7YspWdeUEjLdzzLdhVI+Zjo8sYxnaC
| aA10xiYFM3vNod70kEyY7fE4f0EyDjEZLk5XB/QkEXLQODwuyVzvsDQp/BHZlNJW
| SNxO6aFUcqnfu1PzXoMH6GQRlPjoXP4uv0SwBq0EFQEJ3NK8qi1rlYc34o8zxc17
| a4fp+xQYFftLDihVAT1lVnFJWCE=
|_-----END CERTIFICATE-----
| rdp-ntlm-info: 
|   Target_Name: FEAST
|   NetBIOS_Domain_Name: FEAST
|   NetBIOS_Computer_Name: DC01
|   DNS_Domain_Name: feast.com
|   DNS_Computer_Name: DC01.feast.com
|   Product_Version: 10.0.17763
|_  System_Time: 2026-11-18T16:17:56+00:00
5985/tcp  open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
5986/tcp  open  ssl/wsmans?   syn-ack ttl 125
9389/tcp  open  mc-nmf        syn-ack ttl 125 .NET Message Framing
47001/tcp open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
49664/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49674/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49675/tcp open  ncacn_http    syn-ack ttl 125 Microsoft Windows RPC over HTTP 1.0
49676/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49687/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49711/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49784/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC



Nmap scan report for 192.168.245.171
PORT      STATE SERVICE       REASON          VERSION
135/tcp   open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 125 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 125
5985/tcp  open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
5986/tcp  open  ssl/wsmans?   syn-ack ttl 125
47001/tcp open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
49664/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49670/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49673/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC

Nmap scan report for 192.168.245.170

PORT      STATE SERVICE       REASON          VERSION
80/tcp    open  http          syn-ack ttl 125 Apache httpd 2.4.58 ((Win64) OpenSSL/3.1.3 PHP/8.2.12)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.58 (Win64) OpenSSL/3.1.3 PHP/8.2.12
|_http-title: CloudSync - Your Ultimate File Synchronization Solution
135/tcp   open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 125 Microsoft Windows netbios-ssn
443/tcp   open  ssl/http      syn-ack ttl 125 Apache httpd 2.4.58 ((Win64)
445/tcp   open  microsoft-ds? syn-ack ttl 125
3306/tcp  open  mysql         syn-ack ttl 125 MariaDB 10.3.23 or earlier 
3389/tcp  open  ms-wbt-server syn-ack ttl 125 Microsoft Terminal Services
5985/tcp  open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
5986/tcp  open  ssl/wsmans?   syn-ack ttl 125
47001/tcp open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
49664/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49671/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49672/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
7.98 seconds

```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

---
## Discovered Credentials

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