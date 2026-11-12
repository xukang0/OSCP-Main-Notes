
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

Root for MS02

# Steps to DC01

Bloodhound shows allextendedright and dsync  tom_admin over OSCP.EXAM

[[Impacket-secretsdump SAM SECURITY SYSTEM NTDS.DIT]] to dump administrator DC01 hash

Login with [[Impacket PsExec]] for DC01 root

# Steps to Frankfurt
### User flag

Found /phpadmin/ and /webmail/. Both lead to login pages

both services has no default creds. phpmyadmin root:{blank} fails

Found an authenticated RCE exploit for phpmyadmin

SNMP walk finds jack:3PUKsX98BMupBiCf

SSH jack not working. Account Disabled. Same for FTP

Jack can login to VESTA port 8083

https://github.com/CSpanias/vesta-rce-exploit
Found a vesta authenticated rce exploit.

Exploits says a root shell is achieved.

cat /home/jack/local.txt
cat /root/proof.txt
### Root flag


# Steps to Charlie
### User flag

ftp anonymous login with folder backup

download and see list of pdfs

exiftool pdf to see list of authors.

Try author:author on Usermin login port 20000

on dashboard says version 1.820

searchsploit Usermin. Find Usermin 1.820 - Remote Code Execution (RCE) (Authenticated) 

EDB 50234. Edit the script with listener_ip and port and use python

get a shell as cassie

lse.sh finds /etc/cron.d/2minutes:*/2 * * * * root cd /opt/admin && tar -zxf /tmp/backup.tar.gz *
### Root flag


# Steps to Pascha
### User flag


### Root flag











