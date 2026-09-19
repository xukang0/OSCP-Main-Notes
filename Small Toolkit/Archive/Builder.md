Jenkins 2.441, script console, privatekey, jenkins decrypt, file read linux, file read jenkins poc

[[Active Notes Template]]
## Provided Credentials
---

```

```

```

```

---
## Open Ports

```powershell
22/tcp   open  ssh     syn-ack ttl 63 OpenSSH 8.9p1 Ubuntu 3ubuntu0.6 (Ubuntu 
8080/tcp open  http    syn-ack ttl 62 Jetty 10.0.18
|_http-server-header: Jetty(10.0.18)
|_http-title: Dashboard [Jenkins]
| http-open-proxy: Potentially OPEN proxy.
|_Methods supported:CONNECTION
|_http-favicon: Unknown favicon MD5: 23E8C7BD78E8CD826C5A6073B15068B1
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

---
## Software Versions

```powershell

```

---
## Discovered Subdomains

---
## Discovered Credentials

---
## Interesting Files/Paths

---
## Attack Ideas

---
## Steps to User.txt

[[Current Affairs Notes Template]]

# Steps to User flag

jenkins wappalyzer finds jenkins version number.

This is a file read POC

Read /proc/self/environ/ to understand home directory

/var/jenkins_home/users/users.xml

Gives us jennifer_12108429903186576833

/var/jenkins_home/users/jennifer_12108429903186576833/config.xml

Config file has a bcrypt hash

john crack the hash for creds jennifer : princess

Access to jenkins dashboard

On the manage jenkins credentials page, view page source, there is a jenkins private key

https://devops.stackexchange.com/questions/2191/how-to-decrypt-jenkins-passwords-from-credentials-xml

This forum tells us at script console, 

println(hudson.util.Secret.fromString("{hash}").getPlainText())

This command will yield the cleartext password

This gives us the ssh privatekey

chmod id_rsa and enter root

userflag inside jennifer and root flag at root

## User Flag

```

```

## Root Flag

```

```