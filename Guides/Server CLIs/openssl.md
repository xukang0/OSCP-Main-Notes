```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `openssl s_client -connect ${ip}:imaps`;

dv.paragraph("```bash\n" + command + "\n```");
```
1 LOGIN tom NMds732Js2761

1 LIST ""*

1 SELECT INBOX

1 FETCH 1 BODY[]
