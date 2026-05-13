```
cd /usr/share/seclists/Miscellaneous/
```

```
python3 -m http.server 8080
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}:8080/grepcredwords.txt`;

dv.paragraph("```bash\n" + command + "\n```");
```

Edit grepcredwords.txt
```
cd /usr/share/seclists/Miscellaneous/
```

```
sudo vim grepcredwords.txt
```