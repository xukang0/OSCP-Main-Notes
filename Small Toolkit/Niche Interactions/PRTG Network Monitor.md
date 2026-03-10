Browsing directories revealed the **PRTG configuration folder**:

C:\ProgramData\Paessler\PRTG Network Monitor\

Key file discovered:

PRTG Configuration.old.bak

Downloaded via FTP:

get "PRTG Configuration.old.bak"

---

# 3. Extracting Credentials from Backup

The `.bak` file contains **stored credentials and configuration data** for PRTG.

Search the file for passwords:

cat "PRTG Configuration.old.bak" | grep password

or open in editor:

less "PRTG Configuration.old.bak"

Discovered credentials similar to:

User: prtgadmin  
Password: <password>

---

FOOTHOLD

From the page we find the version to be 18.1.37. A Google search about the vulnerabilities yields a CVE for versions < 18.1.39 (CVE-2018-9276). According to this article, RCE can be achieved while triggering notifications. Let’s try exploiting it. The software by default runs as SYSTEM. Click on Setup > Account Settings > Notifications

Now click on “Add new notification” on the extreme right.

Leave the default fields as they are and scroll down to the "Execute Program" section. We can add a user to Administrators group using this command:

