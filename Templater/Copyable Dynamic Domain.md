```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `${discoveredDomain}`;

dv.paragraph("```bash\n" + command + "\n```");
```
