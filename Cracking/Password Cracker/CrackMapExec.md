```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `crackmapexec smb ${ip} -u [userlist] -p '[passwd]' --local-auth`;

dv.paragraph("```bash\n" + command + "\n```");
```
