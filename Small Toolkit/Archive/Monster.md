[[Active Notes Template]]
## Provided Credentials
---

```
Username:	mike
Email:	mike@monster.pg
```

```
Username:	admin
Email:	wazowski@monster.pg
```

---
## Open Ports

```powershell
80/tcp    open  http          Apache httpd 2.4.41 ((Win64) OpenSSL/1.1.1c PHP/7.3.10)
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/2.4.41 (Win64) OpenSSL/1.1.1c PHP/7.3.10
|_http-title: Mike Wazowski
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
443/tcp   open  ssl/http      Apache httpd 2.4.41 ((Win64) OpenSSL/1.1.1c PHP/7.3.10)
|_http-server-header: Apache/2.4.41 (Win64) OpenSSL/1.1.1c PHP/7.3.10
|_http-title: Mike Wazowski
| tls-alpn: 
|_  http/1.1
| http-methods: 
|_  Potentially risky methods: TRACE
| ssl-cert: Subject: commonName=localhost
| Not valid before: 2009-11-10T23:48:47
|_Not valid after:  2019-11-08T23:48:47
|_ssl-date: TLS randomness does not represent time
445/tcp   open  microsoft-ds?
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
| ssl-cert: Subject: commonName=Mike-PC
| Not valid before: 2026-08-11T07:37:34
|_Not valid after:  2027-02-10T07:37:34
| rdp-ntlm-info: 
|   Target_Name: MIKE-PC
|   NetBIOS_Domain_Name: MIKE-PC
|   NetBIOS_Computer_Name: MIKE-PC
|   DNS_Domain_Name: Mike-PC
|   DNS_Computer_Name: Mike-PC
|   Product_Version: 10.0.19041
|_  System_Time: 2026-08-12T07:43:27+00:00
|_ssl-date: 2026-08-12T07:43:43+00:00; 0s from scanner time.
5040/tcp  open  unknown
7680/tcp  open  pando-pub?
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC

```

---
## Software Versions

```powershell

Domain  MIKE-PC

OS: Windows 10, Windows Server 2019, Windows Server 2016
OS version: '10.0'
OS release: '2004'
OS build: '19041'
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

User is mike

use engineered cracklist to figure out password is "wazowski"

Use Monstra 3.0.4 CVE authenticated RCE to get code execution

Use revshells to generate powershell cmd to catch reverse shell

---
## Steps to root.txt

Winpeas.exe reveals running process `C:\xampp\apache\bin\httpd.exe` . Checking `C:\xampp\properties.ini` showed XAMPP version 7.3.10.

searchsploit -m 50337

geenrate malicious exe with [[msfvenom]]

Transfer to target 

Following the exploit’s PowerShell commands to replace the `xampp-control.ini` configuration file, I successfully obtained a reverse shell as SYSTEM.

Press enter or click to view image in full size

---
## User Flag

```

```

## Root Flag

```

```