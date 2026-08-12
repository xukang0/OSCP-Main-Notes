```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `cadaver http://${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
