**Step 3: Investigate suspicious PIDs**

Suppose you find PID 492.

```
ls -la /proc/492/
```

Interesting files:

|File|What it tells you|
|---|---|
|`cmdline`|Command used to launch process|
|`exe`|Executable being run|
|`cwd`|Current working directory|
|`environ`|Environment variables|
|`status`|UID, GID, capabilities, process information|
|`fd/`|Open file descriptors|
|`maps`|Memory mappings|

Useful commands:

```
cat /proc/492/cmdline | tr '\0' ' '
```

```
readlink -f /proc/492/exe
```

```
readlink -f /proc/492/cwd
```

```
cat /proc/492/status
```

```
ls -la /proc/492/fd/
```

Note: Access to some of these files may be restricted by permissions or kernel security settings.

## **3. What are you looking for during privilege escalation?**

These are the things worth investigating:

|Finding|Potential opportunity|
|---|---|
|Root process executing unusual script|Script modification / hijacking|
|Root process with interesting arguments|Credentials or sensitive paths|
|Credentials in environment variables|Credential reuse|
|Interesting open file descriptors|Sensitive files or sockets|
|Root process using writable executable|Potential code execution|
|Interesting memory contents|Credential extraction|

## **4. My recommended OSCP checklist**

I'd put this in your Linux privilege escalation enumeration notes:

**Process enumeration**

```
# Running processes
ps auxww

# Process tree
ps -ef --forest

# Root processes
ps auxww | grep '^root'

# Search for interesting processes
pgrep -af 'password|mysql|ssh|python|bash'

# Inspect specific PID
ls -la /proc/<PID>/

# Process executable
readlink -f /proc/<PID>/exe

# Process command line
cat /proc/<PID>/cmdline | tr '\0' ' '

# Environment variables
cat /proc/<PID>/environ | tr '\0' '\n'

# Open file descriptors
ls -la /proc/<PID>/fd/
```

Important

**Don't blindly enumerate every PID directory.** Start with `ps auxww`, identify interesting processes, then investigate their corresponding `/proc/PID/` directories.