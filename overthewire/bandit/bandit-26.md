We're still stuck inside of vim from the last bandit. We've already set the
shell. We can't exit vim or else we'll be exited. We'll have to run our
commands from inside vim.

Let's see what files we have.

```sh
:!ls
bandit27-do  text.txt
```

Let's see what bandit27-do does.

```sh
:!./bandit27-do
Example: ./bandit27-do id
```

From the name of the file, it looks like it'll execute a command as bandit27.

Let's get the password for bandit27.

```sh
:!./bandit27-do cat /etc/bandit_pass/bandit27
3ba3118a22e93127a4ed485be72ef5ea
```
