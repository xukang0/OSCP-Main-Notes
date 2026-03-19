IP::   10.129.226.249

| Machine | IP Address | Notes |
| ------- | ---------- | ----- |
|         |            |       |

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
KALI IP::  10.10.16.66
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `${KaliIP}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Web Address
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `http://${ip}/`;

dv.paragraph("```bash\n" + command + "\n```");
```
Discovered Web Domain::   EXAMPLECOM
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `http://${discoveredDomain}/`;

dv.paragraph("```bash\n" + command + "\n```");
```
[[Editing Page]]

wget from local python server
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}:8000/[file]`;

dv.paragraph("```bash\n" + command + "\n```");
```
## Provided Credentials
---
-u daniel 
```
HotelBabylon23
```

```

```

---


## Open Ports
---

| Port | Service | Notes |
| ---- | ------- | ----- |
| 22   |         |       |
| 80   |         |       |

---

## Discovered Subdomains
---


---

## Discovered Credentials
---

| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---

## Attack Angles
---


---

## User Flag

```

```

## Root Flag

```

```