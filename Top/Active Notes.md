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
PORT      STATE SERVICE       VERSION
21/tcp    open  ftp           FileZilla ftpd 0.9.41 beta
| ftp-syst: 
|_  SYST: UNIX emulated by FileZilla
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
3306/tcp  open  mysql         MariaDB 10.3.24 or later (unauthorized)
4443/tcp  open  http          Apache httpd 2.4.43 ((Win64) OpenSSL/1.1.1g PHP/7.4.6)
|_http-server-header: Apache/2.4.43 (Win64) OpenSSL/1.1.1g PHP/7.4.6
| http-title: Welcome to XAMPP
|_Requested resource was http://192.168.151.53:4443/dashboard/
5040/tcp  open  unknown
8080/tcp  open  http          Apache httpd 2.4.43 ((Win64) OpenSSL/1.1.1g PHP/7.4.6)
|_http-open-proxy: Proxy might be redirecting requests
| http-title: Welcome to XAMPP
|_Requested resource was http://192.168.151.53:8080/dashboard/
|_http-server-header: Apache/2.4.43 (Win64) OpenSSL/1.1.1g PHP/7.4.6
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC

Host script results:
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2026-06-22T11:54:32
|_  start_date: N/A

TRACEROUTE (using port 135/tcp)
HOP RTT      ADDRESS
1   47.56 ms 192.168.45.1
2   47.53 ms 192.168.45.254
3   47.58 ms 192.168.251.1
4   40.19 ms 192.168.151.53

```

---
## Software Versions

```powershell
PHP 7.4.6

Windows NT SLORT 10.0 build 19042 (Windows 10) AMD64 x64

OpenSSL 1.1.1g
```

---
## Discovered Subdomains

---
## Discovered Credentials

---
## Interesting Files/Paths

	C:\Apache24\conf/openssl.cnf 

C:\Users\rupert\AppData\Local 

	C:\Users\rupert\OneDrive
AMD64 

	\\SLORT  LOGON SERVER

---
## Attack Ideas

---
## Steps to User.txt

http://192.168.123.53:4443/dashboard shows xampp page.

PHPInfo page can be accessed. 

Feroxbuster port 4443 /site found.

RFI usuable, msfvenom payload RFI grab triggers reverse shell to slort/rupert

at C:\Backup, TFTE.EXE can be deleted and run every 5 minutes

Craft windows reverse shell on kali attacker and transfer onto target

TFTE.EXE executes and triggers admin shell

---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```