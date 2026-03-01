
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `gobuster dir --url http://${ip}/ --wordlist /usr/share/wordlists/dirb/big.txt`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo gobuster vhost -u http://${ip} -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt --append-domain`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
sudo gobuster dir -u <TARGET_URL> -x php,html,css,js,txt,pdf -w <WORDLIST>
```

-x file switch

![[Pasted image 20250512173422.png]]

```
cd ~/Desktop
```

```
gedit pattern
```

```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `gobuster vhost -u http://${ip} -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-110000.txt -p pattern -t 20`;

dv.paragraph("```bash\n" + command + "\n```");
```

General purpose /admin wordlist
```
/usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt
```
