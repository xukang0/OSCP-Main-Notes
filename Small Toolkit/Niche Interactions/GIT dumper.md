Start external python environment

```
python3 -m venv .venv
```

``` 
source .venv/bin/activate
```

---

Install Git Dumper

```
pip install git-dumper
```

---
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `git-dumper http://${ip}/.git ~/.git`;

dv.paragraph("```bash\n" + command + "\n```");
```
