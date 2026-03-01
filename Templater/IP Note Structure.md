```dataviewjs
const page = dv.page("Templater/IP")
dv.paragraph(page.IP)
```

```
```dataviewjs
const page = dv.page("Templater/IP");
const ip = page.IP;
dv.paragraph(`sudo nmap -sV ${ip}`);
```

EXAMPLE :
```dataviewjs
const page = dv.page("Templater/IP");
const ip = page?.IP ?? "NO IP FOUND";
const command = `hydra -l lazie -P /usr/share/wordlists/rockyou.txt ${ip} imap`;

dv.paragraph("```bash\n" + command + "\n```");
```

COPYABLE DYNAMIC IP CMD DIRECT COPY :

```
```dataviewjs
const page = dv.page("Templater/IP");
const ip = page?.IP ?? "NO IP FOUND";
const command = `hydra -l lazie -P /usr/share/wordlists/rockyou.txt ${ip} imap`;

dv.paragraph("```bash\n" + command + "\n```");
```