The password is the only line of text that occurs only once.

We obviously will have to use "uniq -u" for this to filter out non-unique lines
and output the only unique line. However, uniq only works for lines in
immediate succession. We'll have to "sort" the file, then pipe it to "uniq -u".

```sh
bandit8@bandit:~$ sort data.txt | uniq -u
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```
