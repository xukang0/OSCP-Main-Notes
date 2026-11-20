[[Windows Playbook]]
[[Active Directory Playbook]]

---

Find out if box is windows or linux
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ping ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
ttl = 61 > Linux
ttl = 126 > Windows

---
# Linux

[[Linux Initial Enumeration]]

#### Initial access stuck

If SSH open, try name:name of any person you find
[[SQL Injection]]
[[Hydra]]

#### General Priv Esc Enumeration


