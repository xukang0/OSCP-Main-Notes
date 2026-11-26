
[[Active Machine Template]]

```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const hosts = [
    { name: "HOST1", fqdn: "HOST1FQDN" },
    { name: "HOST2", fqdn: "HOST2FQDN" },
    { name: "HOST3", fqdn: "HOST3FQDN" },
    { name: "HOST4", fqdn: "S1FQDN" },
    { name: "HOST5", fqdn: "S2FQDN" },
    { name: "HOST6", fqdn: "S3FQDN" }
];

const table = dv.container.createEl("table");
table.style.width = "100%";
table.style.borderCollapse = "collapse";

const header = table.createEl("tr");

["Machine", "IP Address", "FQDN", "Notes"].forEach(name => {
    const th = header.createEl("th", { text: name });
    th.style.textAlign = "left";
    th.style.padding = "8px";
});

function createCopyButton(cell, value) {
    const text = String(value ?? "").trim();

    const button = cell.createEl("button", {
        text: text || "—"
    });

    button.style.cssText = `
        font-family: monospace;
        cursor: ${text ? "pointer" : "default"};
        padding: 4px 8px;
        opacity: ${text ? "1" : "0.5"};
    `;

    if (!text) return;

    button.addEventListener("click", async () => {
        try {
            await navigator.clipboard.writeText(text);
            button.textContent = "Copied!";
            setTimeout(() => button.textContent = text, 1000);
        } catch {
            button.textContent = "Copy failed";
            setTimeout(() => button.textContent = text, 1000);
        }
    });
}

// Machine rows
for (const host of hosts) {
    const machine = page?.[host.name];
    const ip = page?.[`${host.name}IP`];
    const fqdn = page?.[host.fqdn];
    const notes = page?.[`${host.name}NOTES`];

    if (![machine, ip, fqdn, notes].some(v => v != null && String(v).trim() !== "")) continue;

    const row = table.createEl("tr");

    row.createEl("td", { text: String(machine ?? "") });

    const ipCell = row.createEl("td");
    createCopyButton(ipCell, ip);

    const fqdnCell = row.createEl("td");
    createCopyButton(fqdnCell, fqdn);

    row.createEl("td", { text: String(notes ?? "") });
}

// Kali row
const kaliRow = table.createEl("tr");
kaliRow.createEl("td", { text: "KALI" });

const kaliIPCell = kaliRow.createEl("td");
createCopyButton(kaliIPCell, page?.["KALI IP"]);

kaliRow.createEl("td", { text: "—" });
kaliRow.createEl("td", { text: "Attacker Machine" });

// Active Machine row
const activeRow = table.createEl("tr");

activeRow.createEl("td", {
    text: String(page?.MACHINE ?? "—")
});

const activeIPCell = activeRow.createEl("td");
createCopyButton(activeIPCell, page?.IP);

const domainCell = activeRow.createEl("td");
createCopyButton(domainCell, page?.["Discovered Web Domain"]);

activeRow.createEl("td", {
    text: "Active Machine"
});
```

MACHINE:: S1
IP:: 192.168.123.110
KALI IP:: 192.168.49.123 
Discovered Web Domain:: 192.168.123.110

---
### `DC01`
HOST1:: DC20
HOST1IP:: 172.16.123.200
HOST1NOTES:: Domain Controller
HOST1FQDN:: dc20.oscp.exam

### `MS02`
HOST2:: SRV22
HOST2IP:: 172.16.123.202
HOST2NOTES::
HOST2FQDN:: srv22.oscp.exam
### `MS01`
HOST3:: MS01
HOST3IP:: 192.168.123.206
HOST3NOTES:: creds
HOST3FQDN:: WS26.oscp.exam
### `S1`
HOST4:: S1
HOST4IP:: 192.168.123.110
HOST4NOTES:: Standalone
S1FQDN::
### `S2`
HOST5:: S2
HOST5IP:: 192.168.123.111
HOST5NOTES:: Standalone
S2FQDN::
### `S3`
HOST6:: S3
HOST6IP:: 192.168.123.112
HOST6NOTES:: Standalone
S3FQDN::