Recursively list out all items in a share (after smbclient anonymous share listing)
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `smbmap -H ${ip} -r (sharename)`;

dv.paragraph("```bash\n" + command + "\n```");
```
Download file from share
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `smbmap -u [username] -p '[passwd]' -H ${ip} --download “[sharename]/[filename]”
`;

dv.paragraph("```bash\n" + command + "\n```");
```
Upload File from share
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `smbmap -H ${ip} --upload [yourfile] "[sharename]\[filename]`;

dv.paragraph("```bash\n" + command + "\n```");
```