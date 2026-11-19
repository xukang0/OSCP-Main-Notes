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
Open 192.168.245.173:135
Open 192.168.245.173:139
Open 192.168.245.173:445
Open 192.168.245.173:5985
Open 192.168.245.173:5986
Open 192.168.245.173:47001
```

Only RPC works with Eric creds

```
PORT      STATE SERVICE       REASON          VERSION
135/tcp   open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 125 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 125
5985/tcp  open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
5986/tcp  open  ssl/wsmans?   syn-ack ttl 125
47001/tcp open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
49664/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49674/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RP
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

 net rpc group members "Domain Admins" -U 'laser.com/Eric.Wallows%EricLikesRunning800' -S 192.168.245.172
LASER\Administrator
LASER\boris.crawford

┌──(kali㉿kali)-[~/Desktop/PEN200/Laser/MS01]
└─$ net rpc group members "Remote Desktop Users" -U 'laser.com/Eric.Wallows%EricLikesRunning800' -S 192.168.245.172
LASER\yulia.weber

┌──(kali㉿kali)-[~/Desktop/PEN200/Laser/MS01]
└─$ ~/Desktop/Tools/nxc-sweep 192.168.245.172  -u 'Eric.Wallows' -p 'EricLikesRunning800' | grep '[+]'
[+] Port 3389 open. Checking rdp ...
RDP                      192.168.245.172 3389   DC01             [+] laser.com\Eric.Wallows:EricLikesRunning800 
[+] Port 389 open. Checking ldap ...
LDAP                     192.168.245.172 389    DC01             [+] laser.com\Eric.Wallows:EricLikesRunning800 
[+] Port 389 open. Checking ldap ...
LDAP                     192.168.245.172 389    DC01             [+] laser.com\Eric.Wallows:EricLikesRunning800 
[+] Port 636 open. Checking ldap ...
LDAP                     192.168.245.172 389    DC01             [+] laser.com\Eric.Wallows:EricLikesRunning800 
[+] Port 5986 open. Checking winrm ...
[+] Port 135 open. Checking wmi ...
RPC                      192.168.245.172 135    DC01             [+] laser.com\Eric.Wallows:EricLikesRunning800 
                                                                                                                    
┌──(kali㉿kali)-[~/Desktop/PEN200/Laser/MS01]
└─$ ~/Desktop/Tools/nxc-sweep 192.168.245.173  -u 'Eric.Wallows' -p 'EricLikesRunning800' | grep '[+]'
[+] Port 445 open. Checking smb ...
SMB                      192.168.245.173 445    MS01             [+] laser.com\Eric.Wallows:EricLikesRunning800 
RPC                      192.168.245.173 135    MS01             [+] laser.com\Eric.Wallows:EricLikesRunning800 
                                                                                                                    
┌──(kali㉿kali)-[~/Desktop/PEN200/Laser/MS01]
└─$ ~/Desktop/Tools/nxc-sweep 192.168.245.174  -u 'Eric.Wallows' -p 'EricLikesRunning800' | grep 



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
[[Current Affairs Notes Template]]

---
# Steps to MS01 

### Root flag

Test given creds with nxc

ldapsearch shows domain name is laser.com

eric creds only work with RPC

net rpc user -U 'laser.com/Eric.Wallows%EricLikesRunning800' -S 192.168.245.172 gives a list of domain users. Add to users

For eric.wallows on MS01 there is a writable share called apps

Try to [[SMB NTLMv2 Relay]]

hash captured

Administrator:500:aad3b435b51404eeaad3b435b51404ee:15759746f66f2da88d58f0160f8ee676:::
Admin:1001:aad3b435b51404eeaad3b435b51404ee:3d560aa3cba6bb673b7ef3a30628bf16:::

use psexec to enter NT authority of .174

Flag on administrator desktop

### Pivoting

There is a pcapng file on Administrator documents. With wireshark, fine Yulia.weber: Yulia@Laser777


---

# Steps to DC01 

### User flag

Can RDP into yulia. local.txt on her desktop

### Root flag

Since yulia has genericwrite over boris

[[[Targeted Kerberoasting]]

dump boris crawford kerberos hash

with john i get boris.crawford : zxcvbnm

nxc sweep shows pwned on winrm dc01

since boris.crawford is domain admin, flag is on his desktop
### Pivoting


# Steps to DC01

### User flag



### Root flag



### Pivoting



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






