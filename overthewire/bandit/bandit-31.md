Like the last ones, let's clone.

```sh
bandit31@bandit:~$ mktemp -d
/tmp/tmp.cszzBn02kb
bandit31@bandit:~$ cd /tmp/tmp.cszzBn02kb
bandit31@bandit:/tmp/tmp.cszzBn02kb$ git clone ssh://bandit31-git@localhost/home/bandit31-git/repo
-snip-
bandit31@bandit:/tmp/tmp.cszzBn02kb$ ls
repo
bandit31@bandit:/tmp/tmp.cszzBn02kb$ cd repo/
bandit31@bandit:/tmp/tmp.cszzBn02kb/repo$ ls
README.md
bandit31@bandit:/tmp/tmp.cszzBn02kb/repo$ cat README.md 
This time your task is to push a file to the remote repository.

Details:
    File name: key.txt
    Content: 'May I come in?'
    Branch: master
```

We have to push a file to the remote repository.

First, let's make the file.

```sh
bandit31@bandit:/tmp/tmp.cszzBn02kb/repo$ echo 'May I come in?' > key.txt
```

Now let's add and push it.

```sh
bandit31@bandit:/tmp/tmp.cszzBn02kb/repo$ git add key.txt 
The following paths are ignored by one of your .gitignore files:
key.txt
Use -f if you really want to add them.
```

Huh. Weird. Let's look at the .gitignore to see why our key isn't able to be
added.

```sh
bandit31@bandit:/tmp/tmp.cszzBn02kb/repo$ cat .gitignore 
*.txt
```

Let's try it again, but this time passing the "-f" flag to force it.

```sh
bandit31@bandit:/tmp/tmp.cszzBn02kb/repo$ git add key.txt -f
```

Make sure all's a-ok.

```sh
bandit31@bandit:/tmp/tmp.cszzBn02kb/repo$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   key.txt
```

Now let's push.

```sh
bandit31@bandit:/tmp/tmp.cszzBn02kb/repo$ git commit
Unable to create directory /home/bandit31/.nano: Permission denied
It is required for saving/loading search history or cursor positions.

Press Enter to continue

[master fc39ceb] x
 1 file changed, 1 insertion(+)
 create mode 100644 key.txt



bandit31@bandit:/tmp/tmp.cszzBn02kb/repo$ git push
-snip-
remote: ### Attempting to validate files... ####
remote: 
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote: 
remote: Well done! Here is the password for the next level:
remote: 56a9bf19c63d650ce78e6ec0354ee45e
remote: 
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote:
```
