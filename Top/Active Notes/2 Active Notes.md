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

[+] smb://ZEUS/SVC_MSSQL$@192.168.162.159 [1] -> NewStyle hashes is: True
Administrator:500:aad3b435b51404eeaad3b435b51404ee:a1fcb4118dfcbf52a53d6299aab57055:::
[+] smb://ZEUS/SVC_MSSQL$@192.168.162.159 [1] -> NewStyle hashes is: True
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
[+] smb://ZEUS/SVC_MSSQL$@192.168.162.159 [1] -> NewStyle hashes is: True
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
[+] smb://ZEUS/SVC_MSSQL$@192.168.162.159 [1] -> NewStyle hashes is: True
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:11ba4cb6993d434d8dbba9ba45fd9011:::
[+] smb://ZEUS/SVC_MSSQL$@192.168.162.159 [1] -> NewStyle hashes is: True
cloudbase-init:1004:aad3b435b51404eeaad3b435b51404ee:3ec413a3c92107884e7c75fb9a0caa84:::
[+] smb://ZEUS/SVC_MSSQL$@192.168.162.159 [1] -> NewStyle hashes is: True
Admin:1005:aad3b435b51404eeaad3b435b51404ee:9035fa4c490df7a171b56b881c410a33:::
[*] smb://ZEUS/SVC_MSSQL$@192.168.162.159 [1] -> Done dumping SAM hashes for host: 192.168.162.159

o.foller has SeImpersonatePrivilege




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