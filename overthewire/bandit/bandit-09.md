The line the password is contained in starts with several "===" characters and
is one of the few human readable strings.

This is an easy grep level. We'll also need to use "strings" beforehand to get
only the human readable strings out of the data file.

```sh
bandit9@bandit:~$ strings data.txt | grep "==="
========== theP`
========== password
L========== isA
========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
```
