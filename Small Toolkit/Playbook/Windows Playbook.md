[[Linux Playbook]]
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
# Windows

### **Credential discovery**

- `cmdkey /list`
- `whoami /all`
- PowerShell history
- Unattended installation files
- `C:\Windows\Panther\`
- `C:\Windows.old\`
- SAM/SYSTEM/SECURITY hives
- Credential Manager
- Saved RDP credentials
- Application configuration files
- IIS configuration files
- Registry-stored credentials

#### General Priv Esc Enumeration
[[LinWinPEAS]]
[[SharpUp.exe]]
[[PowerUp.ps1]]
[[0 Seatbelt.exe]]
[[WES-NG]]
