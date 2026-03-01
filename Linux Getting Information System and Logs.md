The `free` command displays information on memory; (`df` (for _disk free*) reports on the available disk space on each of the disks mounted in the file system.

Its `-h` option (for *human readable_) converts the sizes into a more legible unit (usually mebibytes or gibibytes).

In a similar fashion, the `free` command supports the `-m` and `-g` options, and displays its data either in mebibytes or in gibibytes, respectively.

```
$ free
              total        used        free      shared  buff/cache   available
Mem:        2052944      661232      621208       10520      770504     1359916
Swap:             0           0           0
$ df
Filesystem     1K-blocks     Used Available Use% Mounted on
udev             1014584        0   1014584   0% /dev
tmpfs             205296     8940    196356   5% /run
/dev/vda1       30830588 11168116  18073328  39% /
tmpfs            1026472      456   1026016   1% /dev/shm
tmpfs               5120        0      5120   0% /run/lock
tmpfs            1026472        0   1026472   0% /sys/fs/cgroup
tmpfs             205296       36    205260   1% /run/user/132
tmpfs             205296       24    205272   1% /run/user/0
```

The `id` command displays the identity of the user running the session along with the list of groups they belong to. 

```
$ id
uid=1000(kali) gid=1000(kali) groups=1000(kali),27(sudo)
```

The `uname -a` command returns a single line documenting the kernel name (`Linux`), the hostname, the kernel release, the kernel version, the machine type (an architecture string such as `x86_64`), and the name of the operating system (`GNU/Linux`). The output of this command should usually be included in bug reports as it clearly defines the kernel in use and the hardware platform you are running on.

```
$ uname -a
Linux kali 5.8.0-kali3-amd64 #1 SMP Debian 5.8.14-1kali1 (2020-10-13) x86_64 GNU/Linux
```