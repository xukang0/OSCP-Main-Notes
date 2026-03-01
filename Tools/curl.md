```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `curl -I http://${ip} -H "Host: app.inlanefreight.local"`;

dv.paragraph("```bash\n" + command + "\n```");
```
