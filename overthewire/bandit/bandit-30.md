Let's clone.

bandit30@bandit:~$ ls
bandit30@bandit:~$ mktemp -d 
/tmp/tmp.tFrke715PH
bandit30@bandit:~$ cd /tmp/tmp.tFrke715PH
bandit30@bandit:/tmp/tmp.tFrke715PH$ git clone ssh://bandit30-git@localhost/home/bandit30-git/repo

Let's see what we have.

bandit30@bandit:/tmp/tmp.tFrke715PH$ ls
repo
bandit30@bandit:/tmp/tmp.tFrke715PH$ cd repo/
bandit30@bandit:/tmp/tmp.tFrke715PH/repo$ ls
README.md
bandit30@bandit:/tmp/tmp.tFrke715PH/repo$ cat README.md 
just an epmty file... muahaha

Branches?

bandit30@bandit:/tmp/tmp.tFrke715PH/repo$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/master

History?

bandit30@bandit:/tmp/tmp.tFrke715PH/repo$ git log
commit 1791c9d4a559bffa4e6e89c15f7723167da10bb8
Author: Ben Dover <noone@overthewire.org>
Date:   Sun Jul 22 15:49:42 2018 +0200

    initial commit of README.md

Maybe there'll be something in refs.

bandit30@bandit:/tmp/tmp.tFrke715PH/repo$ git show-ref
1791c9d4a559bffa4e6e89c15f7723167da10bb8 refs/heads/master
1791c9d4a559bffa4e6e89c15f7723167da10bb8 refs/remotes/origin/HEAD
1791c9d4a559bffa4e6e89c15f7723167da10bb8 refs/remotes/origin/master
f17132340e8ee6c159e0a4a6bc6f80e1da3b1aea refs/tags/secret

And we have a lead: refs/tags/secret. Let's look at what that has to say.

bandit30@bandit:/tmp/tmp.tFrke715PH/repo$ git show refs/tags/secret 
47e603bb428404d265f59c42920d81e5

Looks like we have the password!
