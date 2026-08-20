```
cd /usr/share/seclists/Miscellaneous/ && python3 -m http.server 8888
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}:8888/grepcredwords.txt`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
grep -Ff grepcredwords.txt -C 2
```

Edit grepcredwords.txt
```
cd /usr/share/seclists/Miscellaneous/
```

```
sudo vim grepcredwords.txt
```

