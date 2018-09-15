Similar to last time. Let's clone.

bandit28@bandit:~$ mktemp -d
/tmp/tmp.J4RvTZTyhg
bandit28@bandit:~$ cd /tmp/tmp.J4RvTZTyhg
bandit28@bandit:/tmp/tmp.J4RvTZTyhg$ git clone ssh://bandit28-git@localhost/home/bandit28-git/repo

Let's see what we have.

bandit28@bandit:/tmp/tmp.J4RvTZTyhg$ ls
repo
bandit28@bandit:/tmp/tmp.J4RvTZTyhg$ cd repo/
bandit28@bandit:/tmp/tmp.J4RvTZTyhg/repo$ ls
README.md
bandit28@bandit:/tmp/tmp.J4RvTZTyhg/repo$ cat README.md 
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx



Looks like the credentials used to be in the file, but was censored. Let's roll
back the repo.

First, let's look at the history of the file.

bandit28@bandit:/tmp/tmp.J4RvTZTyhg/repo$ git log README.md
commit 04e2414585ba775805a49b78d662d0946d08f27a
Author: Morla Porla <morla@overthewire.org>
Date:   Sun Jul 22 14:47:13 2018 +0200

    fix info leak

commit 196c3edc79e362fe89e0d75cfeef079d8c67beef
Author: Morla Porla <morla@overthewire.org>
Date:   Sun Jul 22 14:47:13 2018 +0200

    add missing data

commit 80383714fa509a363756866425b0b697e87824a0
Author: Ben Dover <noone@overthewire.org>
Date:   Sun Jul 22 14:47:13 2018 +0200

    initial commit of README.md



Looks like commit 04e2414585ba775805a49b78d662d0946d08f27a was when they fixed
the info leak. Let's roll it back to the commit before then.

bandit28@bandit:/tmp/tmp.J4RvTZTyhg/repo$ git checkout 196c3edc79e362fe89e0d75cfeef079d8c67beef
-snip-
HEAD is now at 196c3ed... add missing data
bandit28@bandit:/tmp/tmp.J4RvTZTyhg/repo$ ls
README.md
bandit28@bandit:/tmp/tmp.J4RvTZTyhg/repo$ cat README.md 
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: bbc96594b4e001778eee9975372716b2
