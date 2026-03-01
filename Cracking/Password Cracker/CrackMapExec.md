```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `crackmapexec smb ${ip} -u [userlist] -p '[passwd]' --local-auth`;

dv.paragraph("```bash\n" + command + "\n```");
```
