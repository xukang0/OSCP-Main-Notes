NMAP
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo nmap -sU --script ipmi-version -p 623 ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Metasploit Version Scan

```
use auxiliary/scanner/ipmi/ipmi_version 
```

Metasploit hash dumping

```
use auxiliary/scanner/ipmi/ipmi_dumphashes 
```
