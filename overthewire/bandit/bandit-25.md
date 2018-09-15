Let's use the SSH key.

```sh
bandit25@bandit:~$ ssh -i bandit26.sshkey bandit26@localhost
```

We get immediately booted out when we log in, though. This is similar to one of
the previous levels in which you had to pass commands through ssh.

Let's see what kind of a shell we're working with here.

```sh
bandit25@bandit:~$ cat /etc/passwd | grep "bandit26"
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
```

Let's see what that shell looks like.

```sh
bandit25@bandit:~$ cat /usr/bin/showtext
#!/bin/sh

export TERM=linux

more ~/text.txt
exit 0
```

We can disrupt more and therefore delay the exit if we minimize our terminal in
order to force more to do what it's supposed to do.

And from here, we can use "v" to access vim from inside of more.

From inside vim, we can set the shell.

```vim
:set shell=/bin/bash
```

Looks like we're gonna have to use vim as our means of communicating with the
shell.
