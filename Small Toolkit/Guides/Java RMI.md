https://github.com/qtc-de/remote-method-guesser#installation

CD to Folder and assemble the package
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `cd ~/Desktop/Tools/Windows/remote-method-guesser && mvn package`;

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

Run the .jar Remote Method Guesser Enumeration
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");

const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";
const IP = page?.IP ?? "NO IP FOUND";const discoveredDomain = page?.["Discovered Web Domain"] ?? "NO DOMAIN FOUND";

const command = `java -jar target/rmg-5.1.0-jar-with-dependencies.jar enum ${IP} [JAVA_PORT]`;

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