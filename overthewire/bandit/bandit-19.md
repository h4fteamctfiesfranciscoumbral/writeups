We have a binary that executes a command as another user.

```sh
bandit19@bandit:~$ ls
bandit20-do
bandit19@bandit:~$ ./bandit20-do     
Run a command as another user.
  Example: ./bandit20-do id
```

We have to find out how to use this to read bandit20's password. Simple enough.
Pass a command into the binary.

```sh
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```
