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
PORT      STATE SERVICE       REASON          VERSION
135/tcp   open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 125 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 125
5040/tcp  open  unknown       syn-ack ttl 125
5985/tcp  open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
5986/tcp  open  ssl/wsmans?   syn-ack ttl 125
47001/tcp open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
49664/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49670/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC

```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

---
## Discovered Credentials

Mimikatz
CLIENT01 : 37cd766f789605754be10d2c42a84af1
o.foller : decca5b9babc228de4cedeb29a6b9abf
cloudbase-init : 3ec413a3c92107884e7c75fb9a0caa84

└─$ cat connection.sql 
$SqlServer    = 'DC01'
$Database     = 'master'
$SqlAuthLogin = 'zeus.corp\db_user'
$SqlAuthPw    = 'Password123!'


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