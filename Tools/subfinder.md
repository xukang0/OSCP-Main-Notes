```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `echo "${ip}" > resolvers.txt`;

dv.paragraph("```bash\n" + command + "\n```");
```

```shell-session
subfinder -d inlanefreight.com -rL resolvers.txt -v
```

