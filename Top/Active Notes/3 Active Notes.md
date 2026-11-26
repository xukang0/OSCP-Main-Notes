[[Active Notes Template]]
## Provided Credentials
---

```
r.andrews
```

```
BusyOfficeWorker890
```

---
## Open Ports

```powershell
┌──(kali㉿kali)-[~/…/OSCP/AD/MS01/enum]
└─$ sudo rustscan -a 192.168.123.206 -b 500 --ulimit 5000 -- -sC -sV -Pn -oN 192.168.123.206_Fast_Rustscan
[sudo] password for kali: 
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
😵 https://admin.tryhackme.com

[~] The config file is expected to be at "/root/.rustscan.toml"
[~] Automatically increasing ulimit value to 5000.

Scanning 192.168.123.206 [19 ports]
Discovered open port 3306/tcp on 192.168.123.206
Discovered open port 135/tcp on 192.168.123.206
Discovered open port 445/tcp on 192.168.123.206
Discovered open port 80/tcp on 192.168.123.206
Discovered open port 3389/tcp on 192.168.123.206
Discovered open port 139/tcp on 192.168.123.206
Discovered open port 443/tcp on 192.168.123.206
Discovered open port 5040/tcp on 192.168.123.206
Discovered open port 49668/tcp on 192.168.123.206
Discovered open port 49671/tcp on 192.168.123.206
Discovered open port 49667/tcp on 192.168.123.206
Discovered open port 49672/tcp on 192.168.123.206
Discovered open port 49670/tcp on 192.168.123.206
Discovered open port 5985/tcp on 192.168.123.206
Discovered open port 49665/tcp on 192.168.123.206
Discovered open port 49666/tcp on 192.168.123.206
Discovered open port 49669/tcp on 192.168.123.206
Discovered open port 49664/tcp on 192.168.123.206
Discovered open port 47001/tcp on 192.168.123.206

PORT      STATE SERVICE       REASON          VERSION
80/tcp    open  http          syn-ack ttl 127 Apache httpd 2.4.58 ((Win64) OpenSSL/3.1.3 PHP/8.2.35)
|_http-server-header: Apache/2.4.58 (Win64) OpenSSL/3.1.3 PHP/8.2.35
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Home - OffSec NIC
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
443/tcp   open  ssl/http      syn-ack ttl 127 Apache httpd 2.4.58 ((Win64) OpenSSL/3.1.3 PHP/8.2.35)
|_http-title: Home - OffSec NIC
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-server-header: Apache/2.4.58 (Win64) OpenSSL/3.1.3 PHP/8.2.35
445/tcp   open  microsoft-ds? syn-ack ttl 127
3306/tcp  open  mysql         syn-ack ttl 127 MariaDB 10.3.23 or earlier (unauthorized)
3389/tcp  open  ms-wbt-server syn-ack ttl 127
| ssl-cert: Subject: commonName=WS26.oscp.exam
| Issuer: commonName=WS26.oscp.exam
| rdp-ntlm-info: 
|   Target_Name: OSCP
|   NetBIOS_Domain_Name: OSCP
|   NetBIOS_Computer_Name: WS26
|   DNS_Domain_Name: oscp.exam
|   DNS_Computer_Name: WS26.oscp.exam
|   DNS_Tree_Name: oscp.exam
|   Product_Version: 10.0.26100
|_  System_Time: 2026-11-26T09:16:28+00:00
5040/tcp  open  unknown       syn-ack ttl 127
5985/tcp  open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 
47001/tcp open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49670/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49671/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
49672/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC

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

80, 135, 139, 443, 445, 3306, 47001,

Some user names on the 80 443 websites

Test callback using domain search but no answer from nc -lvnp

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