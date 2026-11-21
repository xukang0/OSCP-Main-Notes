[[Active Machine Template]]

```dataviewjs
const machines = [
    ["", "10.10.245.152", ""],
    ["MS01", "192.168.245.153", "creds"],
    ["", "10.10.245.154", ""],
    ["S1", "192.168.245.156", ""],
    ["S2", "192.168.245.157", ""],
    ["S3", "192.168.245.155", ""]
];

const table = dv.container.createEl("table");
table.style.width = "100%";

const header = table.createEl("tr");

["Machine", "IP Address", "Notes"].forEach(name => {
    header.createEl("th", { text: name });
});

for (const [machine, ip, notes] of machines) {
    const row = table.createEl("tr");

    row.createEl("td", { text: machine });
    
    const ipCell = row.createEl("td");
    const button = ipCell.createEl("button", {
        text: ip
    });

    button.style.cursor = "pointer";

    button.addEventListener("click", async () => {
        try {
            await navigator.clipboard.writeText(ip);
            button.textContent = "Copied!";
            setTimeout(() => button.textContent = ip, 1000);
        } catch (error) {
            button.textContent = "Copy failed";
        }
    });

    row.createEl("td", { text: notes });
}
```

MACHINE:: Nagoya
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const machine = page?.MACHINE ?? "NO MACHINE FOUND";

const command = `${machine}`;

dv.paragraph("```bash\n" + command + "\n```");
```
IP::  192.168.132.21
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
KALI IP::  192.168.45.186
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `${KaliIP}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Discovered Web Domain::   nagoya-industries.com
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");
const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `http://${discoveredDomain}/`;

dv.paragraph("```bash\n" + command + "\n```");
```