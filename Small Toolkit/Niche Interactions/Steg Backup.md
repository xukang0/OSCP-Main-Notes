```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `wget http://${ip}/irked.jpg`;

dv.paragraph("```bash\n" + command + "\n```");
```

```
steghide extract -p UPupDOWNdownLRlrBAbaSSss -sf irked.jpg
```

