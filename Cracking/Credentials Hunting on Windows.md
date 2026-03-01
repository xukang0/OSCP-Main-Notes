
Find files containing these file types + the keyword Password
```cmd-session
findstr /SIM /C:"password" *.txt *.ini *.cfg *.config *.xml *.git *.ps1 *.yml
```

For example, to search for both `"password"` **and** `"GitLab"`:

```
findstr /SIM /C:"password" /C:"GitLab" *.txt *.ini *.cfg *.config *.xml *.git
```

```

If you want **files containing both terms simultaneously**, you’d need to pipe `findstr` twice:

`findstr /SIM /C:"password" *.txt *.ini *.cfg *.config *.xml *.git *.ps1 *.yml`