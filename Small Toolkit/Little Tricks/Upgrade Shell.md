```
python3 -c 'import pty;pty.spawn("/bin/bash")'
```

The web-related files are usually stored in the /var/www/html folder, so that's where we are going start.

```
cd /var/www/html
```

```
script /dev/null -c bash
```

