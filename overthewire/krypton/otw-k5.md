Let's look at what we're working with.

```sh
krypton5@krypton:~$ cd /krypton/krypton5/
krypton5@krypton:/krypton/krypton5$ ls
README  found1  found2  found3  krypton6
```

This is the same as last time, but the key length is unknown. Let's use that
same tool from the previous level.

We find the key to be "KEYZEBGLH", which I realize is "KEYLENGTH".

Now let's get the flag...

```sh
krypton5@krypton:/krypton/krypton5$ cat krypton6 
BELOS Z
```

...and decrypt it using Vigenere and the key "KEYLENGTH". We find the flag to
be "RANDO M". "RANDOM".
