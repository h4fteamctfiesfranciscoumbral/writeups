Similar to the last few. Let's clone.

```sh
bandit29@bandit:~$ mktemp -d
/tmp/tmp.cz3tm7O5YE
bandit29@bandit:~$ cd /tmp/tmp.cz3tm7O5YE
bandit29@bandit:/tmp/tmp.cz3tm7O5YE$ git clone ssh://bandit29-git@localhost/home/bandit29-git/repo
-snip-
bandit29@bandit:/tmp/tmp.cz3tm7O5YE$ ls
repo
bandit29@bandit:/tmp/tmp.cz3tm7O5YE$ cd repo/
bandit29@bandit:/tmp/tmp.cz3tm7O5YE/repo$ ls
README.md
bandit29@bandit:/tmp/tmp.cz3tm7O5YE/repo$ cat README.md 
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>



Let's look at the history of this repo.

bandit29@bandit:/tmp/tmp.cz3tm7O5YE/repo$ git log
commit 279d73d37ee7abbe68a3ec3655ef47bdd0d2ebf2
Author: Ben Dover <noone@overthewire.org>
Date:   Sun Jul 22 14:47:23 2018 +0200

    fix username

commit 0ffeba0f812ef30dcd949a3aae1575270b9a7b06
Author: Ben Dover <noone@overthewire.org>
Date:   Sun Jul 22 14:47:23 2018 +0200

    initial commit of README.md
```

Let's look around the initial commit.

```sh
bandit29@bandit:/tmp/tmp.cz3tm7O5YE/repo$ git revert --abort 
bandit29@bandit:/tmp/tmp.cz3tm7O5YE/repo$ git checkout 0ffeba0f812ef30dcd949a3aa
-snip-
bandit29@bandit:/tmp/tmp.cz3tm7O5YE/repo$ ls
README.md
bandit29@bandit:/tmp/tmp.cz3tm7O5YE/repo$ cat README.md 
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit29
- password: <no passwords in production!>
```

Huh. Nothing. Let's go back to the master.

```sh
bandit29@bandit:/tmp/tmp.cz3tm7O5YE/repo$ git checkout master
```

Let's look at all the branches.

```sh
bandit29@bandit:/tmp/tmp.cz3tm7O5YE/repo$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/dev
  remotes/origin/master
  remotes/origin/sploits-dev
```

If there are no passwords in PRODUCTION, then I can bet that the passwords are
in DEV.

```sh
bandit29@bandit:/tmp/tmp.cz3tm7O5YE/repo$ git checkout remotes/origin/dev
-snip-
bandit29@bandit:/tmp/tmp.cz3tm7O5YE/repo$ ls
README.md  code
bandit29@bandit:/tmp/tmp.cz3tm7O5YE/repo$ cat README.md 
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: 5b90576bedb2cc04c86a9e924ce42faf
```
