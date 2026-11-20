[[Active Machine Template]]

| Machine | IP Address      | Notes |
| ------- | --------------- | ----- |
|         | 10.10.106.140   |       |
|         | 192.168.106.141 | creds |
|         | 10.10.106.142   |       |
| S 1     | 192.168.106.143 |       |
| S 2     | 192.168.106.144 |       |
| S 3     | 192.168.106.145 |       |

MACHINE:: OSCPA2/AD
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const machine = page?.MACHINE ?? "NO MACHINE FOUND";

const command = `${machine}`;

dv.paragraph("```bash\n" + command + "\n```");
```
IP::   IP
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
KALI IP::  KALIIP
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `${KaliIP}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Discovered Web Domain::   EXAMPLECOM
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `http://${discoveredDomain}/`;

dv.paragraph("```bash\n" + command + "\n```");
```