# /.git files

## Install Git Dumper

Start external python environment

```
python3 -m venv .venv && source .venv/bin/activate && pip install git-dumper
```

---
## Dump out .git into current directory
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `git-dumper http://${discoveredDomain}/.git gitdump`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

## Running git commands in KALI ATTACKER

```
cd gitdump
```

then run these commands

---
## Check git log

```
git log
```

---
## Show git commit

```
git show [Commit ID]
```

---
## Check git status

```
git status
```

---
## Restore git

```
git restore --staged . && git diff
```

