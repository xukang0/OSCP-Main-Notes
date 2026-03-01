1.  Associate [[IP]]
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `IP=${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```

2. Nmap scan
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo nmap -sC -sV -oA nmap/[boxname] ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```

