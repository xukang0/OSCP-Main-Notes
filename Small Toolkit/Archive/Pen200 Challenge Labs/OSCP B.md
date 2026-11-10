
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
139/tcp   open  netbios-ssn   
syn-ack ttl 64 Microsoft Windows netbios-ssn
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

Get a list of user accounts then use bloodhound to find out who is high value target. And also test all creds again.

RID brute with Eric Creds finds nothing on both MS01 and MS02

Spraying list of users with Eric password gives nothing

Asrep roast against DC doesnt work

nxc sweep against MS02 using Eric Creds show MSSQL validated.

On bloodhound, since there are SVC accounts, kerberoast DC01.

Get kerb hashes and crack with john for creds

get sql_svc creds, login mssql database and xp_cmdshell cmd execution

get RCE on kali for sql_svc

get SAM and SECURITY in windows.old

impacket psexec for root on MS02

# Steps to DC01

Logged in as tom_admin.

Bloodhound shows GenericAll over dc01.oscp.exam. 

[[RBCD]] and get root on DC01

Proof.txt on administrator desktop

# Steps to Kiero
### User flag

UDP snmp open

[[Synced OSCP Notes/Tools/SNMP|SNMP]]

┌──(kali㉿kali)-[~/Desktop/PEN200/OSCPB/Kiero]
└─$ snmpwalk -v2c -c public 192.168.162.149 .1.3.6.1.4.1.8072.1.3
iso.3.6.1.4.1.8072.1.3.2.1.0 = INTEGER: 1
iso.3.6.1.4.1.8072.1.3.2.2.1.2.5.82.69.83.69.84 = STRING: "./home/john/RESET_PASSWD"
iso.3.6.1.4.1.8072.1.3.2.2.1.3.5.82.69.83.69.84 = ""
iso.3.6.1.4.1.8072.1.3.2.2.1.4.5.82.69.83.69.84 = ""
iso.3.6.1.4.1.8072.1.3.2.2.1.5.5.82.69.83.69.84 = INTEGER: 5
iso.3.6.1.4.1.8072.1.3.2.2.1.6.5.82.69.83.69.84 = INTEGER: 1
iso.3.6.1.4.1.8072.1.3.2.2.1.7.5.82.69.83.69.84 = INTEGER: 1
iso.3.6.1.4.1.8072.1.3.2.2.1.20.5.82.69.83.69.84 = INTEGER: 4
iso.3.6.1.4.1.8072.1.3.2.2.1.21.5.82.69.83.69.84 = INTEGER: 1
iso.3.6.1.4.1.8072.1.3.2.3.1.1.5.82.69.83.69.84 = STRING: "Resetting password of kiero to the default value"
iso.3.6.1.4.1.8072.1.3.2.3.1.2.5.82.69.83.69.84 = STRING: "Resetting password of kiero to the default value"
iso.3.6.1.4.1.8072.1.3.2.3.1.3.5.82.69.83.69.84 = INTEGER: 1
iso.3.6.1.4.1.8072.1.3.2.3.1.4.5.82.69.83.69.84 = INTEGER: 0
iso.3.6.1.4.1.8072.1.3.2.4.1.2.5.82.69.83.69.84.1 = STRING: "Resetting password of kiero to the default value"


and find kiero username. means kiero:kiero

Gain access to ftp using those creds. Download id_rsa inside

chmod 600 id_rsa and ssh -i id_rsa john@target and gain john shell. local.txt on his user dir

### Root flag

Can't sudo -l due to no pw

Linpeas shows dirtypipe kernel exploit

Get rootz /root/proof.txt

# Steps to Berlin
### User flag

Check FTP access first

Visit webpage

https://github.com/Goultarde/CVE-2022-42889-text4shell

get RCE

### Root flag

linpeas shows JDWP.

https://github.com/IOActive/jdwp-shellifier/tree/master

[[jdwp-shellifier]]

Chisel port forward 8000.

Chisel port forward 5000 (Trigger server) based on /opt/

run script with cmd to change bin bash perms

Trigger 5000 with nc -nv IP 5000

Go back onto dev and /bin/bash -p for root

# Steps to Gust
### User flag

Nmap scan shows FreeSwitch. 

FreeSWITCH 1.10.1 - Command Execution
https://www.exploit-db.com/exploits/47799

run the exploit with payload windows, powershell -e and base64 encode gets RCE

user chris

flag on his desktop

### Root flag











