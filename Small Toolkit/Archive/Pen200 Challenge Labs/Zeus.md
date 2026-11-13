
[[Current Affairs Notes Template]]

---
# Steps to MS01 

### User flag

135/tcp   open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
139/tcp   open  netbios-ssn   syn-ack ttl 125 Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds? syn-ack ttl 125
5040/tcp  open  unknown       syn-ack ttl 125
5985/tcp  open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
5986/tcp  open  ssl/wsmans?   syn-ack ttl 125
47001/tcp open  http          syn-ack ttl 125 Microsoft HTTPAPI httpd 2.0 
49664/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49665/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49666/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49667/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49668/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49669/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC
49670/tcp open  msrpc         syn-ack ttl 125 Microsoft Windows RPC

enum4linux-ng shows domain name zeus.corp

Computer name is CLIENT01

SMB has a share named SQL

Eric.Wallows is a domain member

Kerberoasting succeeds and shows nothing : No svc accounts?

nxc sweep shows win-rm, rpc, and smb pwned. (all services)

SMB eric creds logon not supported

Evilrm into eric.wallows. Run Mimikatz

CLIENT01$ : 37cd766f789605754be10d2c42a84af1 validates with nxc sweep

o.foller only works for RPC

since client01 has smb sql read and write access try psexec. Doesnt work

Connection.sql has creds for DC01 MSSQL

### Root flag

Realize Eric.Wallows shell has SeImpersonatePrivilege. Become NT authority and root

Flag on administrator desktop

o.foller hash and creds on nxc sweep shows winrm p3wned

---

# Steps to MS02 

### User flag

Enter o.foller through winrm

### Root flag

o.follower has [[SeImpersonatePrivilege]], [[SharpEfsPotato]]

Flag on administrator desktop

# Steps to DC01

### User flag

There is an onboarding document on z.thomas desktop

bloodhound says z.thomas has genericall to D.Chambers

z.thomas :  ^1+>pdRLwyct]j,CYmyi

nxc sweep says z.thomas has winrm access to DC01

User flag on z.thomas desktop

### Root flag

z.thomas has genericall over D.Chambers. 

Change his password and nxc shows it works

Log into winrm using D.Chambers.

Whoami /priv shows SeBackup

get DC root



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






