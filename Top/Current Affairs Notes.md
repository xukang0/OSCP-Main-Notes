
[[Current Affairs Notes Template]]

# Steps to MS01 

sudo gedit /etc/hosts IP address to oscp.exam

nxc sweep with eric wallows creds show SMB and WinRM pwned

No windows.old 

No ldap for bloodhound

Ipconfig shows no internal subnet

Feroxbuster port 8000 of MS01. There is http://ip:8000/partner/db which downloads an sql db to my system. Open it with [[Sqlite]]

Use the .recover function. Get creds

use crackstation to get creds for "support" Freedom1

Checking with nxc_sweep, SSH p3wned with these creds. Enter SSH

Enter as ms01\support

WinPeas shows internal network

Ligolo using support account. Ping MS02 and DC01 it works.

Run nxc sweep on MS02. Eric.Wallows has access to mssql on MS02

impacket-mssqlclient 'Eric.Wallows':EricLikesRunning800@10.10.162.154 -windows-auth to get into MSSQL. : rabbithole

./admintool.exe error shows the source code which includes a valid hash

crackstation this hash for password December31

nxc says administrator:December31 works for SSH

Root for MS01

# Steps to MS02 

### User flag

Check powershell history of all users in root MS01

administrator : hghgib6vHT3bVWf

This allows access into mssql user sql_svc

RCE to gain a shell

Download PSUpload.ps1 + upload SAM and SECURITY into kali (technical errors, revert machine to fix. Run 3 commands at once and 3 listeners)

Impacket secretsdump to get tom_admin hash

use tom_admin creds to psexec into MS02 root

# Steps to DC01



# Steps to Kiero
### User flag


### Root flag


# Steps to Berlin
### User flag



### Root flag



# Steps to Gust
### User flag


### Root flag











