We've gotta look for a certain program being run via cron. Let's see what's
running.

```sh
bandit21@bandit:~$ cd /etc/cron.d/
bandit21@bandit:/etc/cron.d$ ls
cronjob_bandit22  cronjob_bandit23  cronjob_bandit24  popularity-contest
```

Looks like we're gonna have to be dealing with "cronjob_bandit22" from the
looks of it.

Let's see what it does.

```sh
bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22 
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

Looks like it's running a file called "cronjob_bandit22.sh". Let's see what
that does.

```sh
bandit21@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh 
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

Looks like it directs the password for bandit22 into a file called
"/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv". Let's read that file.

```sh
bandit21@bandit:/etc/cron.d$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
```
