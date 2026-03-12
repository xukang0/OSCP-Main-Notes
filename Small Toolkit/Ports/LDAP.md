These devices store LDAP and SMB credentials, in order for the printer to query the user list from Active Directory, and to be able to save scanned files to a user drive. These configuration pages typically allow the domain controller or file server to be specified. Let's stand up a listener on port 389 (LDAP) and specify our tun0 IP address in the Server address field.

```
sudo nc -lvnp 389
```

