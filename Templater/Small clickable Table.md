```dataviewjs
const command = `wmic service get name,startname,pathname`;

const table = dv.container.createEl("table");
table.style.width = "100%";

// Header
const header = table.createEl("tr");
header.createEl("th", { text: "Services" });

// Command row
const row = table.createEl("tr");
const cell = row.createEl("td");

const button = cell.createEl("button", {
    text: command
});

button.style.cursor = "pointer";

button.addEventListener("click", async () => {
    try {
        await navigator.clipboard.writeText(command);
        button.textContent = "Copied!";
        setTimeout(() => button.textContent = command, 1000);
    } catch (error) {
        button.textContent = "Copy failed";
    }
});
```