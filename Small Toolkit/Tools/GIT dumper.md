```
wget https://raw.githubusercontent.com/arthaud/git-dumper/refs/heads/master/git_dumper.py
```

Also installed in 
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `python3 ~/Desktop/Tools/git_dumper.py http://${ip}/.git gitdump`;

dv.paragraph("```bash\n" + command + "\n```");
```

---
Start external python environment

```
python3 -m venv .venv && source .venv/bin/activate && pip install git-dumper
```

---

Install Git Dumper

---

Dump out .git into current directory
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `git-dumper http://${discoveredDomain}/.git gitdump`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

Check git status

```
git status
```

---

Restore git

```
git restore --staged . && git diff
```

