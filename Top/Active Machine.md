[[Active Machine Template]]

| Machine | IP Address      | Notes                      |
| ------- | --------------- | -------------------------- |
| 1       | 172.16.162.10   | DC01                       |
| 2       | 172.16.162.11   | FILES02                    |
| 3       | 192.168.162.120 |                            |
| 4       | 192.168.162.121 | ROOT web02.dmz.medtech.com |
| 5       | 192.168.162.122 |                            |
| 6       | 172.16.162.12   | DEV04                      |
| 7       | 172.16.162.13   | PROD1                      |
| 8       | 172.16.162.14   |                            |
| 9       | 172.16.162.82   | CLIENT01                   |
| 10      | 172.16.162.83   | CLIENT02                   |

MACHINE:: Medtech/Machine1
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const machine = page?.MACHINE ?? "NO MACHINE FOUND";

const command = `${machine}`;

dv.paragraph("```bash\n" + command + "\n```");
```
IP::   192.168.162.121
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
KALI IP::  192.168.45.178
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `${KaliIP}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Discovered Web Domain::   192.168.162.121
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `http://${discoveredDomain}/`;

dv.paragraph("```bash\n" + command + "\n```");
```