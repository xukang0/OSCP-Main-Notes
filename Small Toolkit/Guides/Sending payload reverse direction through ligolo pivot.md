# Sending payload reverse direction MS02 > Kali (MS02 > MS01 > Kali)

Agent listener — callbacks to Kali  
**Scenario:** Kali can reach a deeper Windows host over Ligolo, but that host **cannot connect directly to Kali's VPN IP**. It _can_ connect to the pivot's internal address.  

Deeper host → PIVOT_INTERNAL_IP:PIVOT_PORT
             → Ligolo agent listener
             → Kali proxy 127.0.0.1:KALI_PORT
             → Kali Netcat/HTTP service
  
In Ligolo Interface

```
listener_add --addr 0.0.0.0:4444 --to 127.0.0.1:4444 --tcp
listener_list
```

EXAMPLE:
This one means connect to MS01:1234 and forward to KALI:80.
```
listener_add --addr 0.0.0.0:1234 --to 127.0.0.1:80
```
Always use both 4444 to be safe 

On the deeper host, generate/execute any suitable callback to `PIVOT_INTERNAL_IP:4444`, **not** `KALI_IP:4444`. The actual payloads and PowerShell UTF-16LE Base64 encoding already live in Reverse Shells > Windows; do not duplicate them here. Options there include PowerShell TCP, Powercat, and a Windows EXE. This works even when the deeper host has **no** `agent.exe` installed.  
Before sending a payload, verify:  

```
Test-NetConnection PIVOT_INTERNAL_IP -Port 4444
```
  
**Port translation is allowed:** `--addr 0.0.0.0:9001 --to 127.0.0.1:8000` makes the pivot listen on 9001 while the Kali service remains on 8000. If binding fails with `access permissions` / `address already in use`, check for an existing service using that pivot port and select a free one. `listener_list` showing _Online_ only means the listener is bound, not that the downstream target reached it or Kali's service received bytes.