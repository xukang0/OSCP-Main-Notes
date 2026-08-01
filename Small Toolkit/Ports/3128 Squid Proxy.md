https://blog.1nf1n1ty.team/hacktricks/network-services-pentesting/3128-pentesting-squid

#### To scan itself on port 80  
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `curl -i --proxy http://${ip}:3128 http://${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### To scan itself on port 443 
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `curl -i --proxy http://${ip}:3128 http://${ip}:443`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### To scan itself on port 8000 
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `curl -i --proxy http://${ip}:3128 http://${ip}:8000`;

dv.paragraph("```bash\n" + command + "\n```");
```
#### To scan itself on port 8080 
```dataviewjs
const page = dv.page("Synced OSCP Notes/Top/Active Machine");const ip = page?.IP ?? "NO IP FOUND";

const command = `curl -i --proxy http://${ip}:3128 http://${ip}:8080`;

dv.paragraph("```bash\n" + command + "\n```");
```

Bash Script to automate scanning
```powershell
#!/bin/bash  
  
# Proxy details  
proxy_address="192.168.x.x"  
proxy_port="3128"  
  
# Target IP and ports  
target_ip="192.168.x.x"  
ports=("80" "443" "8000" "8080") #Feel free to add additional ports in the same format  
  
# Loop over ports  
for port in "${ports[@]}"; do  
# Make a request using curl with the proxy, and save the response and status code  
response=$(curl -s -o /dev/null -w "%{http_code}" --proxy $proxy_address:$proxy_port $target_ip:$port)  
  
# Check if the status code is 200  
if [ "$response" -eq 200 ]; then  
echo "Response from $target_ip:$port with status code $response"  
fi  
done
```