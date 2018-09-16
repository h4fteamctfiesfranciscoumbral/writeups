Let's see here...

```sh
leviathan6@leviathan:~$ ls
leviathan6
leviathan6@leviathan:~$ ./leviathan6 
usage: ./leviathan6 <4 digit code>
leviathan6@leviathan:~$ ./leviathan6 1234
Wrong
```

Looks like we're gonna have to bruteforce the file.

```sh
leviathan6@leviathan:~$ for i in {0000..9999}; do ./leviathan6 $i; done
Wrong
Wrong
Wrong
Wrong
-snip-
$
```

And we have shell!

```sh
$ whoami
leviathan7
$ cat /etc/leviathan_pass/leviathan7
ahy7MaeBo9
```
