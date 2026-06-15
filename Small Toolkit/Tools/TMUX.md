## VPN

Start TMUX session
```
tmux new -s vpn
```
### Step 2: Start your VPN

```
sudo openvpn --config seasonalHTB.ovpn
```

### Step 3: Detach from the session (Put it in the background)

Default is Ctrl B
```
Ctrl A + D
```

### How to manage your background VPN later

- **To see active sessions:**
```
tmux ls
```

  Reattach
```
tmux a -t vpn
```

 Kill VPN

```
tmux kill-session -t vpn
```
# Your actual workflow (OSCP style)

## 1. Get initial access (SSH or shell)

Example:

```
ssh user@target-ip
```

Now you are **inside the remote machine**.

---

## 2. Start tmux on the remote machine

```
tmux new -s work
```

That creates a session named `work`.

Now everything you run is inside tmux.

---

## 3. Do your work inside tmux

Examples:

```
nmap -p- 10.10.10.5nc -lvnp 4444python3 exploit.py
```

Everything is now “protected” by tmux.

---

### Run linpeas in one pane

```
./linpeas.sh
```

---

### Split pane (inside tmux)

```
Ctrl+B %
```


---

# 4. Even better: multiple tmux windows

Instead of splits:

### Create new window:

```
Ctrl+B C
```

Switch:

```
Ctrl+B N   (next)Ctrl+B P   (previous)
```

Now you can do:

```
Window 1 → linpeasWindow 2 → manual enumWindow 3 → privesc
```

This is cleaner than splitting everything.

## 4. Disconnect safely anytime

You can leave in 2 ways:

### Detach (clean way)

```
Ctrl + B, then D
```

You are back to your SSH session shell, but tmux keeps running.

### Or just close SSH

Even if you close terminal, tmux keeps running on remote machine.

---

## 5. Reconnect later

SSH back into the same machine:

```
ssh user@target-ip
```

---

## 6. Reattach to tmux session

```
tmux attach -t work
```

Now you are back EXACTLY where you left off.

---

# Mental model (important)

Think:

```
SSH = doorway into machinetmux = room inside machine where work happens
```

- You still need SSH every time
- tmux is what preserves the “room state”

---

# Full cycle summary

```
1. ssh into box2. tmux new -s work3. run tools4. detach (or disconnect)5. ssh back in later6. tmux attach -t work
```