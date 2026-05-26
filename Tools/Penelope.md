https://github.com/brightio/penelope

```
cd ~/Desktop/Tools && python3 penelope.py -p [port] -O / --oscp-safe
```

(Penelope) > help

```
penelope                          # Listening for reverse shells on 0.0.0.0:4444
penelope -p 5555                  # Listening for reverse shells on 0.0.0.0:5555
penelope -p 4444,5555             # Listening for reverse shells on 0.0.0.0:4444 and 0.0.0.0:5555
penelope -i eth0 -p 5555          # Listening for reverse shells on eth0:5555
penelope -a                       # Listening for reverse shells on 0.0.0.0:4444 and show sample reverse shell payloads

penelope -c target -p 3333        # Connect to a bind shell on target:3333

penelope ssh user@target          # Get a reverse shell from target on local port 4444
penelope -p 5555 ssh user@target  # Get a reverse shell from target on local port 5555
penelope -i eth0 -p 5555 -- ssh -l user -p 2222 target  # Get a reverse shell from target on eth0, local port 5555 (use -- if ssh needs switches)

penelope -s <File/Folder>         # Share a file or folder via HTTP
```