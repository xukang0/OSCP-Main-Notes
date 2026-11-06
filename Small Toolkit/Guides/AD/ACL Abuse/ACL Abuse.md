# GenericAll

"Full Control" over the target object. You own it completely.

**If target is a User:** 

**If target is a Group:** Add yourself/any user to that group.

- **Change the Target’s Password**: Using `net user <username> <password> /domain`, the attacker can reset the user’s password.

- **Add Themselves to the Domain Admins Group**: This can be done via direct commands or using modules like Active Directory or PowerSploit.

Check if account is enabled through bloodhound

- GenericAll over a user: Force reset their password.
1. Try Shadow Credentials first.
    
- GenericAll over a computer: 
1. Shadow Credentials 
2. [[RBCD]].
    
- GenericAll over a group: Shadow Credentials isn't the appropriate default; investigate group membership modification.