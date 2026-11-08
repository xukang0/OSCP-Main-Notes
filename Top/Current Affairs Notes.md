
[[Current Affairs Notes Template]]

# Steps to AD SET

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

In C:\Windows.old\Windows\System32\ there is SAM and SECURITY

Download and run impacket

Get hashes

Use psexec to enter tom_admin and become DC

# Steps to Aero




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


