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
Open 192.168.213.66:80
Open 192.168.213.66:135
Open 192.168.213.66:139
Open 192.168.213.66:445
Open 192.168.213.66:5040
Open 192.168.213.66:8082
Open 192.168.213.66:9092
Open 192.168.213.66:49664
Open 192.168.213.66:49665
Open 192.168.213.66:49666
Open 192.168.213.66:49667
Open 192.168.213.66:49668
Open 192.168.213.66:49669

PORT      STATE SERVICE       REASON          VERSION
80/tcp    open  http          syn-ack ttl 125 Microsoft IIS httpd 10.0
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: H2 Database Engine (redirect)
135/tcp   open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 125 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 125
5040/tcp  open  unknown       syn-ack ttl 125
8082/tcp  open  http          syn-ack ttl 125 H2 database http console
|_http-favicon: Unknown favicon MD5: D2FBC2E4FB758DC8672CDEFB4D924540
|_http-title: H2 Console
| http-methods: 
|_  Supported Methods: GET POST
9092/tcp  open  XmlIpcRegSvc? syn-ack ttl 125
49664/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC

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

Port 80 : H2 Database Engine
H2 Database 1.4.196 - Remote Code Execution                                       | java/webapps/45506.py

Port 8082 : H2 Console



---
## Steps to User.txt

On 8082 H2 console, the login form is prefilled for us user "sa" pw empty. This brings us to dashbaord



---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```