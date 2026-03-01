Each file or directory has specific permissions for three categories of users:

- Its owner (symbolized by `u`, as in User).
- Its owner group (symbolized by `g`, as in Group), representing all the members of the group.
- The others (symbolized by `o`, as in Other).

Three types of rights can be combined:

- Reading (symbolized by `r`, as in Read).
- Writing (or modifying, symbolized by `w`, as in Write).
- Executing (symbolized by `x`, as in eXecute).


- `chown user file` changes the owner of the file.
- `chgrp group file` alters the owner group.
- `chmod rights file` changes the permissions for the file.