The web-related files are usually stored in the /var/www/html folder, so that's where we are going start.

```
cd /var/www/html
```

```
script /dev/null -c bash
```

---

```
python -c 'import pty; pty.spawn("/bin/bash")'
```

which python3

```
python3 -c 'import pty; pty.spawn("/bin/bash")'
```


press Ctrl Z

```
stty raw -echo; fg
```

enter

enter

![[Pasted image 20250624232508.png]]

