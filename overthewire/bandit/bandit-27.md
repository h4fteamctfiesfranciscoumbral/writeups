There's a git repo at ssh://bandit27-git@localhost/home/bandit27-git/repo.

Let's clone it.

```sh
bandit27@bandit:~$ mktemp -d
/tmp/tmp.6LQV60ZgvI
bandit27@bandit:~$ cd /tmp/tmp.6LQV60ZgvI
bandit27@bandit:/tmp/tmp.6LQV60ZgvI$ git clone ssh://bandit27-git@localhost/home/bandit27-git/repo
```

The password is the same as for bandit27.

Now let's see what we have.

```sh
bandit27@bandit:/tmp/tmp.6LQV60ZgvI$ ls
repo
bandit27@bandit:/tmp/tmp.6LQV60ZgvI$ cd repo/
bandit27@bandit:/tmp/tmp.6LQV60ZgvI/repo$ ls
README
bandit27@bandit:/tmp/tmp.6LQV60ZgvI/repo$ cat README 
The password to the next level is: 0ef186ac70e04ea33b4c1853d2526fa2
```
