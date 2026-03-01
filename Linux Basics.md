`pwd` command (_print working directory_) displays your current location in the filesystem. 

The current directory is changed with the `cd directory` command (`cd` is for _change directory_). 

When you don't specify the target directory, you are taken to your home directory. 

When you use `cd -` (dash), you go back to the former working directory (the one in use before the last `cd` call). 

The parent directory is always called `..` (two dots), whereas the current directory is also known as `.` (one dot).

The `ls` command allows _listing_ the contents of a directory. If you don't provide parameters, `ls` operates on the current directory.

```
$ pwd
/home/kali
$ cd Desktop
$ pwd
/home/kali/Desktop
$ cd .
$ pwd
/home/kali/Desktop
$ cd ..
$ pwd
/home/kali
$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
```

You can create a new directory with `mkdir directory`

Remove an existing (empty) directory with `rmdir directory`.

`mv` command allows _moving_ and renaming files and directories; 

_removing_ a file is achieved with `rm file`

Copying a file is done with `cp source-file target-file`.

```
$ mkdir test
$ ls
Desktop    Downloads  Pictures  Templates  Videos
Documents  Music      Public    test
$ mv test new
$ ls
Desktop    Downloads  new       Public     Videos
Documents  Music      Pictures  Templates
$ rmdir new
$ ls
Desktop    Downloads  Pictures  Templates  Videos
Documents  Music      Public
```

`type` command lets you query the type of each command.

```
$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
$ which ls
/bin/ls
$ type rm
rm is /bin/rm
$ type cd
cd is a shell builtin
```

Note the usage of the `echo` command, which simply displays a string on the terminal.

The `cat file` command (_concatenate_) reads a file and displays its contents on the terminal.

The `editor` command starts a text editor and allows creating, modifying, and reading text files. 

`command > file` creates a file named file containing the output of the given command. 

`command >> file` is similar except that it appends the output of the command to the file rather than overwriting it.

```
$ echo "Kali rules!" > kali-rules.txt
$ cat kali-rules.txt
Kali rules!
$ echo "Kali is the best!" >> kali-rules.txt
$ cat kali-rules.txt
Kali rules!
Kali is the best!
```

The `find directory criteria` command searches for files in the hierarchy under directory according to several criteria. 

The most commonly used criterion is `-name filename`, which allows searching for a file by name. 

You can also use common wildcards such as "`*`" in the filename search.

```
$ find /etc -name hosts
/etc/hosts
/etc/avahi/hosts
$ find /etc -name "hosts*"
/etc/hosts
/etc/hosts.allow
/etc/hosts.deny
/etc/avahi/hosts
```

The `grep expression files` command searches the contents of the files and extracts lines matching the regular expression. 

Adding the `-r` option enables a recursive search on all files contained in the directory. This allows you to look for a file when you only know a part of its contents.



The `ps aux` command lists the processes currently running and helps to identify them by showing their PID. 

Once you know the _PID_ of a process, the `kill -signal pid` command allows you to send it a signal (if you own the process). 

Several signals exist; most commonly used are `TERM` (a request to terminate gracefully) and `KILL` (a forced kill).

The command interpreter can also run programs in the background if the command is followed by `&`.

By using the ampersand, you resume control of the shell immediately even though the command is still running (hidden from view as a background process).

The `jobs` command lists the processes running in the background; running `fg %job-number` (for _foreground_) restores a job to the foreground. When a command is running in the foreground (either because it was started normally, or brought back to the foreground with `fg`),

the **Control+Z** key combination pauses the process and resumes control of the command line.

The process can then be restarted in the background with `bg %job-number` (for _background_).


