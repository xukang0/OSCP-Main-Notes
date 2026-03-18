cat /root/.ssh/id_rsa

Copy Private Key into id_rsa file using gedit

```
chmod 600 id_rsa
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = `ssh root@${ip} -i id_rsa`;

dv.paragraph("```bash\n" + command + "\n```");
```
