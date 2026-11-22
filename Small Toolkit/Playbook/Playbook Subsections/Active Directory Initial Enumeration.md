Add IPs to ip.txt

---
Add hosts to /etc/hosts 
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `echo "${IP} ${discoveredDomain}" | sudo tee -a /etc/hosts`;

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
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 250);
    } catch {
        button.textContent = "Copy failed";
    }
});
```

---
# Port Scanning

### TCP Scan

Full Rustscan TCP Scan
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo rustscan -a ${ip} -b 500 --ulimit 5000 -- -sC -sV -Pn -oN ${ip}_Fast_Rustscan`;

dv.paragraph("```bash\n" + command + "\n```");
```
(Slower) Full Rustscan TCP Scan
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo rustscan -a ${ip} -b 100 --ulimit 5000 --timeout 5000 -- -sC -sV -Pn -oN ${ip}_Slow_Rustscan`;

dv.paragraph("```bash\n" + command + "\n```");
```
Rustscan TCP Multiple IPs
```
sudo rustscan -a ip.txt -b 500 --ulimit 5000 -- -sC -sV -Pn --append-output -oN all_hosts.txt
```

Nmap TCP double check
```
sudo nmap -sS -p- -Pn -A -n -T3 -iL ip.txt -oN nmap_scan
```

### UDP Scan
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `sudo nmap -sU -sS -sV --top-ports 20 --max-retries 1 -Pn -oN ${ip}_udp ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Nmap UDP Multiple IPs
```
sudo nmap -iL ip.txt -sU -sS -sV --version-intensity 0 --top-ports 20 --max-retries 1 -T4 -Pn -oN udp_scan
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
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `smbclient //${ip}/share -U 'user%pass'`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### LDAP Enumeration
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `nxc ldap ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `ldapsearch -x -H ldap://${ip} -s base namingcontexts`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

[[Web Enumeration Protocol]]