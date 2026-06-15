cat /root/.ssh/id_rsa

Copy Private Key into id_rsa file using gedit

```
chmod 600 id_rsa
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ssh root@${ip} -i id_rsa`;

dv.paragraph("```bash\n" + command + "\n```");
```
Clean dirty id_rsa

```
perl -pe 's/\\n/\n/g' id_rsa > id_rsa.clean
```

or

Clean, format, and wrap the key in one go
```
cat id_rsa | sed -e 's/\\n/\n/g' -e 's/"//g' | fold -w 64 > id_rsa.clean
```

Then check
```
chmod 600 id_rsa.clean && ssh-keygen -l -f id_rsa.clean
```

finally

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ssh root@${ip} -i id_rsa.clean`;

dv.paragraph("```bash\n" + command + "\n```");
```
