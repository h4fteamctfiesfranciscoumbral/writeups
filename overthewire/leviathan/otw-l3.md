Let's see what we're working with here.

```sh
leviathan3@leviathan:~$ ls
level3
leviathan3@leviathan:~$ ./level3 
Enter the password> ^C
leviathan3@leviathan:~$ file level3   
level3: setuid ELF 32-bit LSB shared object, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=01dcd65bfc1afa58036f0100acbce686868f204f, not stripped
```

Looks like another password level. Let's run ltrace on it like we did with the
other password level.

```sh
leviathan3@leviathan:~$ ltrace ./level3 
__libc_start_main(0x565557b4, 1, 0xffffd754, 0x56555870 <unfinished ...>
strcmp("h0no33", "kakaka")                       = -1
printf("Enter the password> ")                   = 20
fgets(Enter the password> x
"x\n", 256, 0xf7fc55a0)                    = 0xffffd560
strcmp("x\n", "snlprintf\n")                     = 1
puts("bzzzzzzzzap. WRONG"bzzzzzzzzap. WRONG
)                       = 19
+++ exited (status 0) +++
```

Looks like it compares our input to "snlprintf". That seems to be the password.

```sh
leviathan3@leviathan:~$ ./level3 
Enter the password> snlprintf
[You've got shell]!
$ whoami
leviathan4
```

Let's get the flag.

```sh
$ cat /etc/leviathan_pass/leviathan4
vuH0coox6m
```
