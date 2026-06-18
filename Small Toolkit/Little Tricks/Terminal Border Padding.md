### Step 1: Create a Custom GTK3 Stylesheet

Open Terminator and check if your local GTK3 user configuration layout folder exists, then open a custom style sheet with nano:

Bash

```
mkdir -p ~/.config/gtk-3.0/
```

```
nano ~/.config/gtk-3.0/gtk.css
```

### Step 2: Paste the Padding Overrides

If the file is blank, that is completely fine. Paste this explicit CSS class selector into the editor:

CSS

```
VteTerminal, TerminalScreen, vte-terminal {
    padding: 7px 12px 7px 12px;
    -VteTerminal-inner-border: 7px 12px 7px 12px;
}
```