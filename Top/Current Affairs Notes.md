
[[Current Affairs Notes Template]]

# Steps to MS01 

Open 192.168.162.147:21
Open 192.168.162.147:22
Open 192.168.162.147:135
Open 192.168.162.147:139
Open 192.168.162.147:445
Open 192.168.162.147:5040
Open 192.168.162.147:5985
Open 192.168.162.147:5986 Evil WINRM
Open 192.168.162.147:7680 
Open 192.168.162.147:8000 INV
Open Inv 192.168.162.147:8080 INV
Open Inv 192.168.162.147:8443 INV
Open 192.168.162.147:47001
Open 192.168.162.147:49670
Open 192.168.162.147:49671
Open 192.168.162.147:49669
Open 192.168.162.147:49668
Open 192.168.162.147:49667
Open 192.168.162.147:49666
Open 192.168.162.147:49665
Open 192.168.162.147:49664

| ssl-cert: Subject: commonName=MS01.oscp.exam
| Subject Alternative Name: DNS:MS01.oscp.exam
| Issuer: commonName=MS01.oscp.exam

Domain is oscp.exam

add to /etc/hosts

Gameplan : 

Investigate open web ports, 
8000 : Default IIS
8080
8443 : 

None of them yield results, attempt to feroxbuster. Nothing.

NXC sweep shows SSH, WinRM, SMB succeeds with Eric.Wallows.

cant access SMB file with Eric creds

SeImpersonatePrivilege on Eric.Wallows [[SeImpersonatePrivilege]]

Use SharpEfsPotato to become NT Authority on MS01

No flags anywhere. 

Try to run bloodhound

Eric.Wallows deadend as well as MS01

Try to ligolo pivot to MS02

Succeed and nmap scan MS02

NT Authority achieved, no flag in this computer. Compromised.

# Steps to MS02 

### User flag

Succeed and nmap scan MS02

135/tcp   open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 64 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 64
1433/tcp  open  ms-sql-s      syn-ack ttl 64 Microsoft SQL Server 2019 
5040/tcp  open  unknown       syn-ack ttl 64
49664/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49670/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49671/tcp open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
49700/tcp open  ms-sql-s      syn-ack ttl 64 Microsoft SQL Server 2019

Ideas : 

Find some creds somewhere for 

MySQL server

or SMB enumeration
