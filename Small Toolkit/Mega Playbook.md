# General

#### Time Sync

```
sudo timedatectl set-ntp false
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo ntpdate -s ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```

Lower MTU rate
`sudo ip l s dev tun0 mtu 1250`

Revert machine
[[Python Detector]]

```
export MS01 = IP
```

[[Locating & Fixing Exploits]]
# Linux

[[Initial Enumeration]]

#### Initial access stuck

If SSH open, try name:name of any person you find
[[SQL Injection]]


---
# Active Directory

#### General

Disable Antivirus
```
Set-MpPreference -DisableRealtimeMonitoring $true
```
Show Hidden Files in Directory
```
dir -Force
```
Check Recycle bin
```
cd '$RECYCLE.BIN'
```

Recycle Bins have two types of files. The ones that start with `$I` store metadata about the file. The `$R` file holds the original content.

[[Synced OSCP Notes/Small Toolkit/Guides/AD/Net|Net]]
[[NXC-Sweep]]

---
#### Initial Enumeration
[[Initial Enumeration]]
Nmap + Web
Initial Domain Enumeration > [[NetExec]]
RPC Domain Enumeration > [[135 RPC]]
SMB Share Enumeration > [[SMB]]

---
#### Initial Access


[[SQL Injection]]
[[Feroxbuster]]
[[AWS s3 bucket]]
[[SMB NTLMv2 Relay]]
[[NTLM Theft]]
[[NTLM Auth]]

RCE shell upload, if RCE shell does not work, try a WWWshell Webshell. Then upload nc64.exe onto system and execute RCE

---
#### If user, looking to gain machine root.

[[Synced OSCP Notes/OSCP Main Notes/Windows/Mimikatz|Mimikatz]]
[[Watch-Command]]
[[Sqlite]]

#### Web
If [[Windows LFI RFI]], call back to [[Responder]] for ntlm hash
[[inetpub]] in file system

Check for value files like lsass.zip

SYSVOL contains Group Policy files, scripts and configuration data. Those can sometimes reveal credentials, service configurations or other weaknesses.

Group Policy Preferences have historically exposed credentials through an attribute called `cpassword` in services.xml

---
#### If admin user, no new creds, looking to move laterally.

[[Bloodhound Startup]]

[[Synced OSCP Notes/OSCP Main Notes/Windows/Mimikatz|Mimikatz]]
[[Rubeus.exe]]
[[Runas]]
[[PSHistory]]
[[Impacket PsExec]]
[[SMB NTLMv2 Relay]]
[[NTLM Theft]]
[[NTLM Auth]]

If you have a list of usernames, but no password
[[ASREP Roasting]]

If you have creds of a domain user, and/discover which SVC accounts exist
[[Kerberoasting]]

[[Active Directory Toolkit|-k nxc kerberos ticket]]

Sometimes the svc account guy has a personal account as well which he reuses the same password for

Autologon
```
reg.exe query "HKLM\software\microsoft\windows nt\currentversion\winlogon"
```
[[Synced OSCP Notes/Small Toolkit/Guides/AD/Windows Credential Manager|Windows Credential Manager]]

Spray existing users and passwords
Same password as user
Crackstation existing hashes

---
#### Creds, what to do?

[[Impacket PsExec]]
[[1433 MSSQL]]
[[NXC-Sweep]]
[[cPassword]]
#### General Priv Esc Enumeration

[[LinWinPEAS]]
[[SharpUp.exe]]
[[PowerUp.ps1]]
[[0 Seatbelt.exe]]
#### Directory Enumeration

[[Impacket-secretsdump SAM SECURITY SYSTEM NTDS.DIT]]

https://github.com/G4sp4rCS/backup-operator-to-domain-admin-POC/tree/main

#### Priv Esc

[[SeImpersonatePrivilege]] > [[SharpEfsPotato]]
[[SeManageVolume]]
[[SeBackupPrivilege]]
[[SeRestorePrivilege]]

Any foreign groups, research.
[[GPO Abuse]]

If Azure spotted, try ADSync
[[Azure Admins Group]]
[[LAPS]]

[[ADCS]]
#### AD/ACL Techniques

[[ACL Abuse]]  
1. [[GenericAll]]  
2. [[GenericWrite]]  
3. [[WriteDACL]]  
4. [[WriteOwner]]  
5. [[ForceChangePassword]]  
  
AD Exploitation  
6. [[CoerceToTGT]]  
7. [[RBCD]]  
8. [[GPO Abuse]]  
9. [[DCSync]]  
10. [[Shadow Credentials]]

#### Have creds, login methods

[[Impacket PsExec]]
[[wmiexec]]
