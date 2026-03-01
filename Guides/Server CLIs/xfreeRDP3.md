RDP TCP/3389
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `xfreerdp3 /u:[USERNAME] /p:'[PASSWORD]' /v:${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
