[[Active Machine Template]]

| Machine | IP Address | Notes |
| ------- | ---------- | ----- |
|         |            |       |

MACHINE:: Monster
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const machine = page?.MACHINE ?? "NO MACHINE FOUND";

const command = `${machine}`;

dv.paragraph("```bash\n" + command + "\n```");
```
IP::   192.168.124.180
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
KALI IP::  192.168.45.161
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `${KaliIP}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Discovered Web Domain::   192.168.124.180
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `http://${discoveredDomain}/`;

dv.paragraph("```bash\n" + command + "\n```");
```