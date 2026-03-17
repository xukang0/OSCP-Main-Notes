```
wget https://raw.githubusercontent.com/arthaud/git-dumper/refs/heads/master/git_dumper.py
```

Also installed in 

```
cd /home/kali/Desktop/MyTools/[git_dumper.py]
```

---
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

Dump out .git into current directory
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `git-dumper http://${ip}/.git gitdump`;

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

