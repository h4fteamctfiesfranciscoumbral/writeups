The binary will connect to a port and see if it receives the current password
from the other side. It will pass the password for bandit21 if it does.

We need two terminals for this. We can use "tmux" to spawn another terminal.

```sh
bandit20@bandit:~$ tmux
```

Then we can press "CTRL+B c" to create a new window.

Now let's open up a port with "nc" (netcat) and pass "-l" (listen).

```sh
bandit20@bandit:~$ nc -l localhost 45921
```

Now let's go back to the previous termianl with "CTRL+B p".

Now let's run the binary.

Now let's go back to the terminal netcat's running on with "CTRL+B n" and pass
the password of the current level.

```sh
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr
```
