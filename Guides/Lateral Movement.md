We can use cat * to read all files while pipeing the output to grep where we provide the pattern of a string that starts with the word passw and followed by any string such as for example words passwd or password. We can also use the switch -i to ignore case sensitive words like Password. 

```
cat * | grep -i passw*
```

```
sudo -l
```

list out cmds allowed

```
cd C:\\Users
```

