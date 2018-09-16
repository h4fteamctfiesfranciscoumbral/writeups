Let's see what we're working with.

```sh
leviathan4@leviathan:~$ ls
leviathan4@leviathan:~$ ls -a
.  ..  .bash_logout  .bashrc  .profile  .trash
leviathan4@leviathan:~$ cd .trash/
leviathan4@leviathan:~/.trash$ ls
bin
leviathan4@leviathan:~/.trash$ file bin 
bin: setuid ELF 32-bit LSB shared object, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=d3808cd51b87c957fdaa96b31a561c7aa414f952, not stripped
```

We've got a binary again. Let's see what it does.

```sh
leviathan4@leviathan:~/.trash$ ./bin 
01010100 01101001 01110100 01101000 00110100 01100011 01101111 01101011 01100101 01101001 00001010
```

That's binary for the flag. Convert it to ASCII and we get Tith4cokei.
