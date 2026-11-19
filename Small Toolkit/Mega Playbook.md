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

[[Synced OSCP Notes/Small Toolkit/Guides/AD/Net|Net]]
[[NXC-Sweep]]

#### Initial Enumeration
[[Initial Enumeration]]
Nmap + Web
#### Initial Access


[[SQL Injection]]
[[Feroxbuster]]
[[AWS s3 bucket]]
[[SMB NTLMv2 Relay]]
[[NTLM Theft]]
[[NTLM Auth]]

RCE shell upload, if RCE shell does not work, try a WWWshell Webshell. Then upload nc64.exe onto system and execute RCE

#### If user, looking to gain machine root.

[[Synced OSCP Notes/OSCP Main Notes/Windows/Mimikatz|Mimikatz]]
[[Watch-Command]]

#### If admin user, looking to move laterally.

[[Bloodhound Startup]]

[[Synced OSCP Notes/OSCP Main Notes/Windows/Mimikatz|Mimikatz]]
[[Rubeus.exe]]
[[PSHistory]]
[[Impacket PsExec]]
[[SMB NTLMv2 Relay]]
[[NTLM Theft]]
[[NTLM Auth]]
[[As-Rep Roasting]]
Spray existing users and passwords
Same password as user
Crackstation existing hashes
#### Creds, what to do?

[[Impacket PsExec]]
[[1433 MSSQL]]
[[NXC-Sweep]]
[[cPassword]]

#### General Priv Esc Enumeration

[[LinWinPEAS]]
[[SharpUp.exe]]
[[PowerUp.ps1]]

#### Directory Enumeration

[[Impacket-secretsdump SAM SECURITY SYSTEM NTDS.DIT]]

https://github.com/G4sp4rCS/backup-operator-to-domain-admin-POC/tree/main

#### Priv Esc

[[SeImpersonatePrivilege]] > [[SharpEfsPotato]]
