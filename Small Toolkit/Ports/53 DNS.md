```
dig 
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `dig @${ip} axfr ${discoveredDomain}`;

dv.paragraph("```bash\n" + command + "\n```");
```



[[DIG]]

[[subfinder]]

[[subbrute]]

```shell-session
host support.inlanefreight.com
```