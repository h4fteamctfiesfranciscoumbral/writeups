Let's see what we're dealing with here.

```sh
leviathan1@leviathan:~$ ls
check
leviathan1@leviathan:~$ ./check 
password: ^C
leviathan1@leviathan:~$ file check 
check: setuid ELF 32-bit LSB shared object, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=a59dfd0a32a6badc54a17cd8e04091fd6f9d049a, not stripped
```

Looks like the binary requires a password as an input. Let's see if we can find
the password that it compares our input to using "ltrace".

```sh
leviathan1@leviathan:~$ ltrace ./check 
__libc_start_main(0x565556c0, 1, 0xffffd754, 0x565557a0 <unfinished ...>
printf("password: ")                             = 10
getchar(0xf7fc5000, 0xffffd754, 0x65766f6c, 0x646f6700password: x
) = 120
getchar(0xf7fc5000, 0xffffd754, 0x65766f6c, 0x646f6700) = 10
getchar(0xf7fc5000, 0xffffd754, 0x65766f6c, 0x646f6700
) = 10
strcmp("x\n\n", "sex")                           = 1
puts("Wrong password, Good Bye ..."Wrong password, Good Bye ...
)             = 29
+++ exited (status 0) +++
```

Here we notice an interesting line. 

```c
strcmp("x\n\n", "sex")
```

Looks like the password that it compares our input to is "sex".

```sh
leviathan1@leviathan:~$ ./check 
password: sex
$ whoami
leviathan2
```

This spawns a shell as leviathan2. Let's get the password for leviathan2.

```sh
$ cat /etc/leviathan_pass/leviathan2
ougahZi8Ta
```
