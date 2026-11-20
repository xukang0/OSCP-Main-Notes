[[Active Notes Template]]
## Provided Credentials
---

```
Eric.Wallows
```

```
EricLikesRunning800
```

---
## Open Ports

```powershell
Open 192.168.245.141:22
Open 192.168.245.141:80
Open 192.168.245.141:81
Open 192.168.245.141:135
Open 192.168.245.141:139
Open 192.168.245.141:445
Open 192.168.245.141:3306
Open 192.168.245.141:3307
Open 192.168.245.141:5040
Open 192.168.245.141:5985
Open 192.168.245.141:5986
Open 192.168.245.141:7680
Open 192.168.245.141:47001
Open 192.168.245.141:49664
Open 192.168.245.141:49665
Open 192.168.245.141:49666
Open 192.168.245.141:49668
Open 192.168.245.141:49667
Open 192.168.245.141:49669
Open 192.168.245.141:49670
Open 192.168.245.141:49713

22/tcp    open  ssh           syn-ack ttl 125 OpenSSH for_Windows_8.1 (protocol 2.0)
80/tcp    open  http          syn-ack ttl 125 Apache httpd 2.4.51 ((Win64) PHP/7.4.26)
| http-methods: 
|   Supported Methods: POST OPTIONS HEAD GET TRACE
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/2.4.51 (Win64) PHP/7.4.26
|_http-title: Home
|_http-generator: Nicepage 4.8.2, nicepage.com
81/tcp    open  http          syn-ack ttl 125 Apache httpd 2.4.51 ((Win64) 
135/tcp   open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 125 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 125
3306/tcp  open  mysql         syn-ack ttl 125 MySQL (unauthorized)
3307/tcp  open  mysql         syn-ack ttl 125 MariaDB 10.3.24 or later 
5040/tcp  open  unknown       syn-ack ttl 125
5985/tcp  open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
5986/tcp  open  ssl/wsmans?   syn-ack ttl 125
7680/tcp  open  pando-pub?    syn-ack ttl 125
47001/tcp open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49670/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49713/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC

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

port 80 and 81 web enumeration

SMB share enumeration

mySQL 3306 3307

---
## Steps to User.txt

Running NXC using Eric.Wallow creds, it says WinRM and SSH pwned




---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```