```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `remmina -c "rdp://[user]:[password]@${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```

Right Ctrl + F to escape fullscreen
