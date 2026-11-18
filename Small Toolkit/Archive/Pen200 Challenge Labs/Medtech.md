[[Current Affairs Notes Template]]

---
# Steps to WEB02 

### Initial access

Nmap scans shows

Machine 3 : SSH, 80
Machine 4: 80, 135, 139, 47001
Machine 5 : SSH 

Looks like the foucs is machine 4. Visit webpage 80. Medtech website. Uses .ASPX. Dir Fuzz.
There is a patient login portal at login.aspx

From enum4linux ng we get some domain information

[+] Found domain information via SMB
NetBIOS computer name: WEB02
NetBIOS domain name: MEDTECH
DNS domain: medtech.com
FQDN: WEB02.dmz.medtech.com
Derived membership: domain member
Derived domain: MEDTECH

Test' on medtech patient portal shows mssql error.

Get RCE to land on nt service\mssql$sqlexpress

### Root flag

SeImpersonatePriv exists [[SharpEfsPotato]]

Flag on Administrator desktop


---
# Steps to FILES02 

### User flag

in joe downloads on WEB02 root, there is test.zip 

Inside contains web.config with creds to user SA.

Realize WEB02 root has access to internel subnet. Ligolo pivot to internal subnet. Nmap scan.

mimikatz lsa secrets dump on web02 root gives joe:Flowers1

nxc winrm on FIles02 shows pwned

Evilwinrm into joe for local.txt
### Root flag

SeImpersonatePriv on FILE02, proof.txt on administrator desktop

Found Yoshi, Wario and Joe

Conduct bloodhound collection

Leon is Domain admin

In PS history i can see that wario creates a credential on CLIENT02



---
# Steps to CLIENT 02

### User flag

Joe has fileBackupMonitoring.log which contains hashes for goomba, daisy, wario, and toad

nxc sweep hashes with username shows wario hash works for client 01, 02, dev4, prod1

Evilwinrm on client 02, tgt with earlier information.

Flag on his desktop

### Root flag

Winpeas shows auditTracker.exe in developmentexecutable

Put msfvenom shell.exe replacing auditTracker.exe and sc.exe start auditTracker to catch reverse shell

land as root

flag on desktop


---
# Steps to CLIENT 01

### User flag

nxc rdp sweep shows wario creds work for client01 and dev04

Also shows yoshi:fdf36048c1cf88f5630381c5e38feb8e pwned against rdp

This has on crack station is Mushroom! so yoshi : Mushroom! and wario : Mushroom!
### Root flag

evil winrm onto yoshi for root flag. 

---
# Steps to DEV04

### User flag

nxc sweep shows yoshi:Mushroom! works for RDP onto DEV04.

Flag on his desktop
### Root flag

There is C:\TEMP\backup.exe

Hijack this exe with shell.exe and get NT authority reverse shell on kali

flag on his desktop

---
# Steps to DC01

### Root Flag

In mimikatz LSA dump there is a default password rabbit:) 

nxc-sweep shows leon:rabbit:) works

nxc-sweep shows winrm validates

Root flag on his desktop

## Prod

using leon creds

# Steps to WEB01

### User flag

there are creds in dc01 leon admin desktop
### Root flag

sudo -l shows (all)

so sudo -i for root

root flag

# Steps to VPN

### User flag

Hydra brute force for offsec:password ssh login.

cat /home/offsec/local.txt
### Root flag

sudo -l shows openvpn

gtfo bins to sudo openvpn and get root

flag on /root/proof.txt

# Steps to NTP

### User flag

on VPN there is mario profile with .ssh

Use id_rsa to enter mario account

flag on his home dir

---

# Steps to Frankfurt
### User flag



### Root flag

---
# Steps to Charlie
### User flag



### Root flag



---
# Steps to Pascha
### User flag



### Root flag








