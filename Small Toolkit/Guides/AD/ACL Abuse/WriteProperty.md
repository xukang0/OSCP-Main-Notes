You can modify a particular AD attribute.

| Writable attribute                         | What you can potentially do                       |
| ------------------------------------------ | ------------------------------------------------- |
| `servicePrincipalName`                     | Add an SPN and perform [[Targeted Kerberoasting]] |
| `member`                                   | Add a member to a group [[AddMember]]             |
| `msDS-AllowedToActOnBehalfOfOtherIdentity` | Configure [[RBCD]]                                |
| `msDS-KeyCredentialLink`                   | Configure [[Shadow Credentials]]                  |

There is no universal WriteProperty command because each attribute has a different purpose.

For example, if you have WriteProperty over the RBCD attribute of a computer, use:
