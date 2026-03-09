# Quick Feroxbuster Guide

## 1️⃣ Basic Scan

feroxbuster -u http://target.com -w /usr/share/wordlists/dirb/common.txt

**What it does**

- `-u` → target URL
- `-w` → wordlist

Example:

feroxbuster -u http://10.10.10.10 -w /usr/share/seclists/Discovery/Web-Content/common.txt

---

# 2️⃣ Recommended Realistic Scan

This is what many pentesters run first.

feroxbuster -u http://target.com \  
-w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt \  
-x php,html,txt,bak \  
-t 50

**Options**

- `-x` → file extensions
    
- `-t` → threads
    

Example output:

200 GET /admin  
200 GET /login.php  
403 GET /backup  
301 GET /images

---

# 3️⃣ Recursive Scanning

Feroxbuster **automatically scans discovered directories**.

Example:

/admin  
/admin/login.php  
/admin/config.php  
/admin/uploads

You don’t need to manually rescan directories like Gobuster.

---

# 4️⃣ Ignore Junk Status Codes

Some servers return lots of useless results.

Example:

feroxbuster -u http://target -w wordlist.txt -C 404,403

Ignore:

404  
403

---

# 5️⃣ Filter By Response Size (VERY useful)

Sometimes everything returns **200 but same size**.

feroxbuster -u http://target -w wordlist.txt --filter-size 1234

Removes responses with that size.

---

# 6️⃣ Scan With Cookies (for authenticated areas)

feroxbuster -u http://target -w wordlist.txt -H "Cookie: PHPSESSID=abc123"

---

# 7️⃣ Save Results

feroxbuster -u http://target -w wordlist.txt -o results.txt

---

# 8️⃣ Smart Scan for HTB / OSCP

A common workflow:

```
feroxbuster -u http://[domain] -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt -x php,html,txt,bak,zip -t 80
```

---

# 🔥 Pro Tip (Many beginners miss this)

Use **multiple wordlists simultaneously**:

feroxbuster -u http://target \  
-w common.txt \  
-w raft-medium-directories.txt

---

# ⚡ Feroxbuster vs Gobuster

|Tool|Strength|
|---|---|
|Gobuster|Simple|
|Feroxbuster|Faster + recursive + filtering|

Most pentesters prefer **Feroxbuster now**.

---

# 🧠 Real HTB Workflow

Usually I run **3 scans in parallel**:

feroxbuster small wordlist  
feroxbuster medium wordlist  
feroxbuster with extensions

---

If you're doing **HackTheBox / OSCP / CPTS boxes**, I can also show you:

- **The exact feroxbuster command top pentesters use**
    
- **Why gobuster sometimes misses files**
    
- **The 3 enumeration scans you should ALWAYS run first**
    

Just say and I'll show you. 🔥