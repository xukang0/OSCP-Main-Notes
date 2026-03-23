ssh jimmy@10.10.10.171 -L 52846:localhost:52846

connect into port 52846

```
http://127.0.0.1:52846/
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `ssh jimmy@${discoveredDomain} -L 8080:localhost:8080`;

dv.paragraph("```bash\n" + command + "\n```");
```
