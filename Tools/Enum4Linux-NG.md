```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `enum4linux-ng -A ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```

enum4linux --help

-a enables all parameters

```shell-session
./enum4linux-ng.py 10.10.11.45 -A -C
```