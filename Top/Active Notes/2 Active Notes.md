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

MSSQL access on MS02

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

Try to priv esc

# MS02 Root




---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```