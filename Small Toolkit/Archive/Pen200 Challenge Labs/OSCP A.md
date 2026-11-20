
[[Current Affairs Notes Template]]

# Steps to AD SET

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

MS01$ : cbe2aba6fb6a9a54c889087fab8afeba

Mary.Williams : 9a3121977ee93af56ebd0ef4f527a35e NO Crack

Celia.Almeda : e728ecbadfb02f51ce8eed753f3ff3fd No Crack

admin : 2f0330d04480d07becb77bdb3bd995a9 no Crack

cloudbase-init : fe0cab7f85305845bc7e016fcd51ee8d No Crack

support : d9358122015c5b159574a88b3c0d2071 Freedom1

Secret  : _SC_wampmariadb64 / service 'wampmariadb64' with username : .\Mary.Williams
cur/text: 69jHwjGN2bPQFvJ no crack

Secret  : DefaultPassword
cur/text: 7k8XHk3dMtmpnC7 no crack

Mysql
    CHANGE MASTER TO MASTER_HOST='125.564.12.1', MASTER_PORT=3306,
;    MASTER_USER='joe', MASTER_PASSWORD='secret';

web_svc : Diamond1



|         |          |
| ------- | -------- |
| support | Freedom1 |


---
## Interesting Files/Paths

---
## Attack Ideas

port 80 and 81 web enumeration SEEN

SMB share enumeration SEEN

mySQL 3306 3307

port 81 attendance and payroll input

Spray creds against all users SEEN

Celia.Almeda has read access to a share called Users on DC01. 

EvilWinRM on MS02 pwned.  SEEN

MSSQL access on MS02 SEEN

---
## Steps to User.txt

Running NXC using Eric.Wallow creds, it says WinRM and SSH pwned. SMB shares visible.

Try to authenticate using SMB Eric Creds. Logon failure. Domain name is oscp.exam. Name of the machine is MS01.

Add these information to /etc/hosts

Since RPC open, try to enumerate domain information

Since we have no access to DC, RPC does not work.

Using nxc smb rid brute force gives us a list of domain users. Add to users

On ms01.oscp.exam port 80, there is a company website. Some additional names to add to users.

Port 81 is an attendance and payroll website. POTENTIALLY interesting

We can enter SSH EricWallows as well as as evilwinrm. Proceed to enumerate his filesystem

On his C:\Users, we see more interesting user accounts. Add to users. There is also a web_svc account.

With ping test, seems like MS01 can reach internal subnet. Ligolo pivot. Tested and I can reach internal subnet

Enumerate internal subnet IPs. Nmap scan both internal ports. 

Notice Eric.Wallows has SeImpersonatePrivilege > [[SharpEfsPotato]]

Gain NT authority on MS01

# Pivoting

Run mimikatz.exe. Found interesting hashes for some user accounts. Attempt to crackstation them.

Seems like Support : Freedom1 is found. Add this to passwords and creds.

nxc spray everything to understand what support can be used for. Unfortunately, support creds doesnt work for SMB

Bloodhound enumeration to understand the system better. Nothing much interesting

Try to spray all hashes against usernames. Celia.Almeda works.

Celia.Almeda has read access to a share called Users on DC01. EvilWinRM on MS02 pwned. MSSQL access on MS02

# MS02 Local

Celia.Almeda can enter MS02 and has user access to MS02

Celia.Almeda can enter MSSQL using PTH but nothing inside

Try to priv esc

Seems like kerberoasting gives kerb hashes for web_svc and sql_svc

Crack the hashes. Web_svc gives Diamond1. SQL_svc cannot be cracked

Found windows.old on C:\ . Get SAM and SECURITY and get hashes

tom_admin seems interesting he is part of domain admins

tom_admin says pwned for smb dc01 and ms02

# DC01 Root

since nxc smb shows tom_admin has read and write access to most smb shares, PSexec to enter tom_admin on DC01.

Succeed and land on administrator DC01. 

Flag on administrator desktop


---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```

# Steps to Aero

port 80, 81, 443, 3000, 3001 all useless

Feroxbuster for ip adress shows /sub and /index.php

/index php tells us pico version number 

Pico 3.0.0-alpha.2.

Feroxbuster /api discoveres /heartbeat

at /api/heartbeat, found aerospike db

searchsploit aerospike db reveals poc

Use poc to get RCE on aero user

LSE.sh shows /usr/bin/screen-4.5.0

POC detailing steps to take for root

/usr/bin/screen priv esc

https://github.com/YasserREED/screen-v4.5.0-priv-escalate

Get root and flag on /root/proof.txt

# Steps to User flag

Running Machine 2 creds using nxc sweep, creds pwned for winrm, ssh, smb shares, 

Use creds for RID brute for a list of users as well (MS01:users1)

Evil win-rm into Eric.Willows. There are a few user accounts inside

Found mysql on ms01.oscp.exam. Error message says this hostname not allowed to connect

Interesting stuff in C:\setup, but ultimately led nowhere

oscp\eric.wallows has SeImpersonatePriv

Enumeration shows machine is windows 10 pro.

SharpEfsPotato works. NT authority/system. Part of Administrators group

Enumerated every single Desktop and Documents of Users

LaZagne gives some hashes

Administrator:500:aad3b435b51404eeaad3b435b51404ee:3c4495bbd678fac8c9d218be4f2bbc7b:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:11ba4cb6993d434d8dbba9ba45fd9011:::
Mary.Williams:1002:aad3b435b51404eeaad3b435b51404ee:9a3121977ee93af56ebd0ef4f527a35e:::
support:1003:aad3b435b51404eeaad3b435b51404ee:d9358122015c5b159574a88b3c0d2071:::
cloudbase-init:1004:aad3b435b51404eeaad3b435b51404ee:cb47daeda02df568b81ca633a210a76a:::
Admin:1005:aad3b435b51404eeaad3b435b51404ee:bd063c2d424044053dadc6a197c8e222:::

Useless.

Use ligolo to reach internal subnet of MS02.

Try nxc-sweep of celia.almeda hash against MS02. Works. 

Nxc shows winrm Pwned. Enter celia almeda



# Steps to Crystal

Ports 21,22 and 80 open

Running feroxbuster against 80, there is /cms/ and /.git/

ftp anonymous login failed

Since .git exists, [[GIT dumper]]

Git logs shows commits, view them and find creds for DB

Breakingbad92

also stuart with the same creds

Attempt username dean against ftp and ssh

Stuart@ip with the password allows access to ftp, where there is local.txt

Stuart@ip allows access to ssh

Running linpeas shows:

1. SUID bit set pkexec
2. ╔══════════╣ Readable files inside /tmp, /var/tmp, /private/tmp, /private/var/at/tmp, /private/var/tmp, and backup folders (limit 70) (T1552.001)
-rw-r--r-- 1 root root 20 Nov  8 15:41 /tmp/netdev.tmp
-rw-rw-r-- 1 stuart stuart 4331 Nov  8 16:21 /tmp/cf31-probe-1528.py
-rw-r--r-- 1 stuart stuart 26890 Apr  5  2018 /opt/backup/sitebackup1.zip
-rw-r--r-- 1 stuart stuart 25312 Mar  5  2020 /opt/backup/sitebackup3.zip
-rw-r--r-- 1 stuart stuart 24701 Nov 18  2022 /opt/backup/sitebackup2.zip

pkexec nope

sitebackup3 zip2john for pw codeblue

7z this file for prompt

chloe : Ee24zIK4cDhJHL4H

su chloe to get root

su chloe has all:all in sudo -l

sudo -i for root

flag in /root/proof.txt


# Steps to Hermes

Allign Clock skew

Note : 
1. MouseServer open
2. Evil Win-rm open
3. RDP open

FTP nothing

Skipped investigating his website

RPC nothing

From Enum4linux :

Anonymous smbclient denied

[+] Found domain information via SMB
NetBIOS computer name: OSCP
NetBIOS domain name: ''
DNS domain: oscp
FQDN: oscp
Derived membership: workgroup member
Derived domain: unknown

OS: Windows 10, Windows Server 2019, Windows Server 2016
OS version: '10.0'
OS release: '2004'
OS build: '19041'

Port 1978 is WifiMouse, [[WifiMouse]] to get oscp/offsec shell.

Flag on user offsec Desktop

## Root

Winpeas shows

 zachary: "&('C:\Program Files\PuTTY\plink.exe') -pw 'Th3R@tC@tch3r' zachary@10.51.21.12 'df -h'"
```
Th3R@tC@tch3r
```

FTP cant
RPC can login but SKIP
SMB yes but only READ to IPC$
Enum4linux nothing
RDP allows me on

Use netcat to get shell of zachary on my kali

whoami is zachary

whoami /groups shows zachary is administrator

Go onto administrator desktop and get proof.txt
