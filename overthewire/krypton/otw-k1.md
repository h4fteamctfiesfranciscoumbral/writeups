Let's see what we're working with. All files for this game are located in
/krypton/.

```sh
krypton1@krypton:~$ cd /krypton/
krypton1@krypton:/krypton$ ls
krypton1  krypton2  krypton3  krypton4  krypton5  krypton6
krypton1@krypton:/krypton$ cd krypton1/
krypton1@krypton:/krypton/krypton1$ ls
README  krypton2
```

Let's see what krypton2 has to say.

```sh
krypton1@krypton:/krypton/krypton1$ cat krypton2 
YRIRY GJB CNFFJBEQ EBGGRA
```

The README file tells us that the file is encrypted using rot13. Easy enough.
I did this before on one of the bandit challenges.

```sh
krypton1@krypton:/krypton/krypton1$ tr "A-Z" "N-ZA-M" < krypton2 
LEVEL TWO PASSWORD ROTTEN
```
