```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `evil-winrm -i ${ip} -u <username> -p <password>`;

dv.paragraph("```bash\n" + command + "\n```");
```
