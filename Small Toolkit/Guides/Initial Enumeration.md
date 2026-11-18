Add hosts to /etc/hosts 
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `echo "${ip} ${discoveredDomain}" | sudo tee -a /etc/hosts`;

dv.paragraph("```bash\n" + command + "\n```");
```
---
# Port Scanning

### TCP Scan

Full Rustscan TCP Scan
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo rustscan -a ${ip} -b 500 --ulimit 5000 -- -sC -sV -Pn`;

dv.paragraph("```bash\n" + command + "\n```");
```
Rustscan TCP Multiple IPs
```
sudo rustscan -a ip.txt -b 500 --ulimit 5000 -- -sC -sV -Pn --append-output -oN all_hosts.txt
```

Nmap TCP double check
```
sudo nmap -sS -p- -Pn -A -n -T3 -iL ip.txt -oA medtech_scan
```

### UDP Scan
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo nmap -sU -sS -sV --top-ports 20 --max-retries 1 -Pn -oA udp_scan ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Nmap UDP Multiple IPs
```
sudo nmap -iL ip.txt -sU -sS -sV --version-intensity 0 --top-ports 20 --max-retries 1 -T4 -Pn -oA udp_scan
```

After finding open ports, consult [[0 Port Number Table]].

Visit https://speedguide.net/ports.php

#### Grab banner name
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `telnet ${ip} [port]`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### NXC enumeration
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `nxc smb ${ip} [port] -u '' -p '' --shares`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `smbclient -L \\\\${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```