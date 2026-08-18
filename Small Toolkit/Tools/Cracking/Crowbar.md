RDP password spraying
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `crowbar -b rdp -s ${ip}/32 -U [usernamefile] -c '[passwd]'`;

dv.paragraph("```bash\n" + command + "\n```");
```

