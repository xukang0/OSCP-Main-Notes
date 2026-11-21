
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
    const text = String(value ?? "");
    const button = cell.createEl("button", {
        text: text || "—"
    });

    button.style.cssText = `
        font-family: monospace;
        cursor: pointer;
        padding: 4px 8px;
    `;

    button.addEventListener("click", async () => {
        if (!text) return;

        try {
            await navigator.clipboard.writeText(text);
            button.textContent = "Copied!";
            setTimeout(() => button.textContent = text, 1000);
        } catch {
            button.textContent = "Copy failed";
        }
    });
}

for (const host of hosts) {
    const machine = page?.[host.name];
    const ip = page?.[`${host.name}IP`];
    const fqdn = page?.[host.fqdn];
    const notes = page?.[`${host.name}NOTES`];

    if (!machine && !ip) continue;

    const row = table.createEl("tr");

    row.createEl("td", { text: String(machine ?? "") });

    const ipCell = row.createEl("td");
    createCopyButton(ipCell, ip);

    const fqdnCell = row.createEl("td");
    createCopyButton(fqdnCell, fqdn);

    row.createEl("td", { text: String(notes ?? "") });
}
```

MACHINE:: MS01

IP:: 192.168.245.141

KALI IP:: 10.10.14.5

Discovered Web Domain:: example.com

---
### `DC01`
HOST1:: DC01
HOST1IP:: 
HOST1NOTES:: Domain Controller
HOST1FQDN::

### `MS02`
HOST2:: MS02
HOST2IP:: 
HOST2NOTES::
HOST2FQDN::
### `MS01`
HOST3:: MS01
HOST3IP:: 
HOST3NOTES:: creds
HOST3FQDN::
### `S1`
HOST4:: S1
HOST4IP:: 
HOST4NOTES:: Standalone
S1FQDN::
### `S2`
HOST5:: S2
HOST5IP:: 
HOST5NOTES:: Standalone
S2FQDN::
### `S3`
HOST6:: S3
HOST6IP:: 
HOST6NOTES:: Standalone
S3FQDN::