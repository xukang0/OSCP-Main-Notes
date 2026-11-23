[[Linux Playbook]]
[[Windows Playbook]]

[[0000021| [PEN200] Initial Setup ]]
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

Fix broken cmd path 
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `set PATH=%SystemRoot%\system32;%SystemRoot%;`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```
[[Synced OSCP Notes/Small Toolkit/Guides/AD/Net|Net]]
[[NXC-Sweep]]

---
#### Initial Enumeration
[[Port Service Enumeration]]
Nmap + Web
Initial Domain Enumeration > [[NetExec]]
RPC Domain Enumeration > [[135 RPC]]
SMB Share Enumeration > [[139 445 SMB]]
[[LDAP Enumeration]]

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
#### Pivoting

Ping Test
```dataviewjs
const command = "Test-NetConnection PIVOT_INTERNAL_IP";

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    await navigator.clipboard.writeText(command);
    button.textContent = "Copied!";
    setTimeout(() => button.textContent = command, 25);
});
```

[[Ligolo]]

---
#### If user, looking to gain machine root.

[[Synced OSCP Notes/Small Toolkit/Guides/AD/Mimikatz|Mimikatz]]
[[Watch-Command]]
[[Sqlite]]
[[Kerberoasting]] > Discover service accounts creds 

#### Web
If [[Windows LFI RFI]], call back to [[Responder]] for ntlm hash
[[inetpub]] in file system

Check for value files like lsass.zip

SYSVOL contains Group Policy files, scripts and configuration data. Those can sometimes reveal credentials, service configurations or other weaknesses.

Group Policy Preferences have historically exposed credentials through an attribute called `cpassword` in services.xml

---
#### If admin user, no new creds, looking to move laterally.

[[Bloodhound Startup]]

##### `Credential Discovery`
[[Autologon]]
[[Synced OSCP Notes/Small Toolkit/Guides/AD/Windows Credential Manager|Windows Credential Manager]]
[[PSHistory]]
[[GPP]] > cPassword
[[Unattended Files]]
[[GMSA]]
[[WinSCP]]
[[FileZilla]]
[[PuTTY]]
[[DPAPI]]
```dataviewjs
const command = "cmdkey /list";

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    await navigator.clipboard.writeText(command);
    button.textContent = "Copied!";
    setTimeout(() => button.textContent = command, 1000);
});
```
Check C:\Users, C:\
dotPEEK > Read .exe (On Native laptop)

##### `Directory Enumeration`
[[Impacket-secretsdump SAM SECURITY SYSTEM NTDS.DIT]] > Check C:\windows.old\Windows\System32

SSH key discovery

Services
```dataviewjs
const command = "wmic service get name,startname,pathname";

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    await navigator.clipboard.writeText(command);
    button.textContent = "Copied!";
    setTimeout(() => button.textContent = command, 1000);
});
```

**Search common configuration and script files:**
```dataviewjs
const command = "Get-ChildItem C:\ -Include *.config,*.ini,*.xml,*.ps1,*.bat,*.cmd -File -Recurse -ErrorAction SilentlyContinue";

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    await navigator.clipboard.writeText(command);
    button.textContent = "Copied!";
    setTimeout(() => button.textContent = command, 1000);
});
```

##### `Dumping`
[[Synced OSCP Notes/Small Toolkit/Guides/AD/Mimikatz|Mimikatz]] > !
[[Rubeus.exe]]
[[Runas]]
[[Impacket PsExec]]
[[SMB NTLMv2 Relay]] > !
[[NTLM Theft]]
[[NTLM Auth]]
[[Synced OSCP Notes/Small Toolkit/Guides/AD/LSASS|LSASS]]

##### `Kerberos Techniques : Service accounts`
[[Pass The Hash (PtH)]]
[[Overpass The Hash]]
[[Pass The Ticket]]
[[Kerberoasting]] > !
[[Silver Ticket]] > If MSSQL and no xp_cmdshell
[[Golden Ticket]] > Post exploitation, only if have krbgt hash

##### Delegation Attacks`
[[Unconstrained Delegation]]
[[Constrained Delegation]]
[[RBCD]]

If you have a list of usernames, but no password
[[ASREP Roasting]] 

If you have creds of a domain user, and/discover which SVC accounts exist
[[Kerberoasting]]

[[Active Directory Toolkit|-k nxc kerberos ticket]]

Sometimes the svc account guy has a personal account as well which he reuses the same password for


Spray existing users and passwords
Same password as user
Crackstation existing hashes

---
#### Creds, what to do?
[[NXC-Sweep]]
[[GPP]]
#### Lateral Movement Login methods
[[Impacket PsExec]] > SMB (445), administrative privileges
[[Synced OSCP Notes/Small Toolkit/Tools/Evil-Winrm|Evil-Winrm]] >  WinRM (5985/5986),  remote shell permissions
[[wmiexec]] > RPC/DCOM connectivity, typically local admin
[[smbexec]]
[[atexec]]
[[xfreeRDP3]] >  RDP (3389), RDP logon permissions
[[DCOM]] > TCP 135 + dynamic RPC + local admin
[[1433 MSSQL]] > impacketmssqlclient

[[winrs]]  > authorised for remote management
[[Remote Powershell]]

---
#### General Priv Esc Enumeration
[[LinWinPEAS]]
[[SharpUp.exe]]
[[PowerUp.ps1]]
[[0 Seatbelt.exe]]
[[WES-NG]]
#### whoami /priv
[[SeImpersonatePrivilege]] > [[SharpEfsPotato]]
[[SeManageVolumePrivilege]]
[[SeBackupPrivilege]]
[[SeRestorePrivilege]]
[[SeDebugPrivilege]]
[[SeTakeOwnershipPrivilege]]

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
6. [[AddMember]]
7. [[AllExtendedRights]]
8. [[WriteProperty]]
9. [[AddSelf]]
  
AD Exploitation  
10. [[CoerceToTGT]]  
11. [[RBCD]]  
12. [[GPO Abuse]]  > WriteGPLink
13. [[DCSync]]  
14. [[Shadow Credentials]]
15. [[LAPS]]

