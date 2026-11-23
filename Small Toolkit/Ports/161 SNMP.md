161
162w
10161
10162

---

SNMP Enumeration
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `snmpwalk -v2c -c public ${ip} .1.3.6.1.4.1.8072.1.3`;

dv.paragraph("```bash\n" + command + "\n```");
```
---

SNMP Bulkwalk Enumeration
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `snmpbulkwalk -c [COMM_STRING] -v [VERSION] ${ip} .`;

dv.paragraph("```bash\n" + command + "\n```");
```
```
snmpbulkwalk -c public -v2c 10.10.11.136 .
```

SEARCH FOR STRING: "Resetting password of kiero to the default value"

means

kiero:kiero

---

SNMP Check Enumeration
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `snmp-check ${ip} -c public`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

**Commands to check processes**  
**Running Processes (**`hrSWRunName`**):** Lists active binaries and services on the target.  
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `snmpwalk -v2c -c public ${IP} 1.3.6.1.2.1.25.4.2.1.2`;

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

  
**Process Arguments (**`hrSWRunParameters`**)**: Often reveals hardcoded passwords, API keys, or custom script paths passed via CLI flags.  
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `snmpwalk -v2c -c public ${IP} 1.3.6.1.2.1.25.4.2.1.5`;

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

  
**Custom Net-SNMP Extensions (**`nsExtendOutputFull`**):** Administrators often attach custom bash scripts to SNMP here (commonly used for backups, status checks, or password resets).  
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `snmpwalk -v2c -c public ${IP} 1.3.6.1.4.1.8072.1.3.2`;

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
  
**Search for credentials, scripts, or reset keywords:**  
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `grep -iE "pass|pwd|admin|reset|script|sh|cron|user" snmpwalk_full.txt`;

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

**Essential Commands to Keep in Your Cheatsheet:**

- **Find Community Strings:**
    
    Bash
    
    ```
    onesixtyone -c /usr/share/seclists/Discovery/SNMP/common-snmp-community-strings.txt <TARGET_IP>
    ```
    
- **Automated Overview:**
    
    Bash
    
    ```
    snmp-check <TARGET_IP> -c public
    ```
    
- **Manual Full Walk:**
    
    Bash
    
    ```
    snmpwalk -v2c -c public <TARGET_IP>
    ```