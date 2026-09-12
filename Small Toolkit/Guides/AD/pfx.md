No file suffix (.pfx)
filename:: 
```dataviewjs
const page = dv.page("Synced OSCP Notes/Small Toolkit/Guides/AD/pfx");
const filename = page?.["filename"] ?? "NO FILENAME FOUND";

const command = `pfx2john ${filename}`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Small Toolkit/Guides/AD/pfx");
const filename = page?.["filename"] ?? "NO FILENAME FOUND";

const command = `openssl pkcs12 -in ${filename}.pfx -nocerts -out ${filename}.key-enc`;

dv.paragraph("```bash\n" + command + "\n```");
```
Enter PEM key : Your own passwords > 4 letters

```dataviewjs
const page = dv.page("Synced OSCP Notes/Small Toolkit/Guides/AD/pfx");
const filename = page?.["filename"] ?? "NO FILENAME FOUND";

const command = `openssl rsa -in ${filename}.key-enc -out ${filename}.key`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Small Toolkit/Guides/AD/pfx");
const filename = page?.["filename"] ?? "NO FILENAME FOUND";

const command = `openssl pkcs12 -in ${filename}.pfx -clcerts -nokeys -out ${filename}.crt`;

dv.paragraph("```bash\n" + command + "\n```");
```
---
Ensure both Cert and key files exist
```dataviewjs
const page = dv.page("Synced OSCP Notes/Small Toolkit/Guides/AD/pfx");
const filename = page?.["filename"] ?? "NO FILENAME FOUND";

const command = `ls ${filename}.*`;

dv.paragraph("```bash\n" + command + "\n```");
```
---
## Evil-WinRM Connection with PFX
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const pagea = dv.page("Synced OSCP Notes/Small Toolkit/Guides/AD/pfx");
const filename = pagea?.["filename"] ?? "NO FILENAME FOUND";

const command = `evil-winrm -i ${discoveredDomain} -S -k ${filename}.key -c ${filename}.crt`;

dv.paragraph("```bash\n" + command + "\n```");
```
