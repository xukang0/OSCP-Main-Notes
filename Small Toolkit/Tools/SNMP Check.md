**snmp-check** is a quick enumeration tool for **SNMP services** (usually UDP port **161**) that automatically pulls useful info like users, running processes, network interfaces, etc.

Here’s a **fast practical guide** you’d use during HTB / pentesting. 🧠

---

# 1️⃣ Basic Usage

```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `snmp-check ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Example:

snmp-check 10.129.231.213

By default it tries the common SNMP community string:

public

---

# 2️⃣ Specify Community String

If you know the community string:

```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `snmp-check -c public ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
Example with a custom one:

snmp-check -c private 10.129.231.213

---

# 3️⃣ Specify SNMP Port

Normally SNMP runs on **UDP 161**, but if different:

```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `snmp-check -p 161 -c public ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

# 4️⃣ What Information It Pulls

If the community string is correct, you can get:

### System information

Hostname  
OS version  
Kernel  
System uptime

### Network interfaces

eth0  
IP addresses  
MAC addresses

### Running processes

apache2  
mysqld  
sshd

### Installed software

### Logged in users

### TCP/UDP connections

### Mounted drives

---

# 5️⃣ Real HTB Workflow

When you discover **UDP 161 open**:

### Step 1

```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `snmp-check ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
### Step 2 (if nothing)

Try common community strings:

```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `snmp-check -c public ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```
```dataviewjs
const page = dv.page("Templater/IP");const ip = page?.IP ?? "NO IP FOUND";

const command = `snmp-check -c private ${ip}`;

dv.paragraph("```bash\n" + command + "\n```");
```

---

# 6️⃣ If You Don’t Know the Community String

Use **onesixtyone**:

onesixtyone -c /usr/share/seclists/Discovery/SNMP/common-snmp-community-strings.txt 10.129.231.213

Then feed the result into `snmp-check`.

---

# 7️⃣ Very Useful Option (clean output)

snmp-check -c public -v 2c 10.129.231.213

`-v` specifies SNMP version.

Most HTB boxes use:

SNMP v1  
SNMP v2c

---

# Quick Example Output

[*] System information:  
  
Hostname:   backup-server  
Contact:    admin@example.com  
Location:   Server Room  
Uptime:     12 days  
  
[*] Network interfaces:  
  
eth0 -> 10.129.231.213  
lo   -> 127.0.0.1