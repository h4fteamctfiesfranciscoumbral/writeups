Let's look at what we're working with.

```sh
krypton2@krypton:~$ cd /krypton/krypton2/
krypton2@krypton:/krypton/krypton2$ ls
README  encrypt  keyfile.dat  krypton3
```

The README tells us that krypton3 is encrypted using the Caesar cipher.

Let's make a temporary directory to work in, as per the README.

```sh
krypton2@krypton:/krypton/krypton2$ mktemp -d
/tmp/tmp.8eNUJXdxnB
krypton2@krypton:/krypton/krypton2$ cd /tmp/tmp.8eNUJXdxnB
krypton2@krypton:/tmp/tmp.8eNUJXdxnB$ ln -s /krypton/krypton2/keyfile.dat
krypton2@krypton:/tmp/tmp.8eNUJXdxnB$ chmod 777 .
```

Alright. Let's generate a key mapping to decrypt the flag.

```sh
krypton2@krypton:/tmp/tmp.8eNUJXdxnB$ echo "ABCDEFGHIJKLMNOPQRSTUVWXYZ" > x
krypton2@krypton:/tmp/tmp.8eNUJXdxnB$ /krypton/krypton2/encrypt x
krypton2@krypton:/tmp/tmp.8eNUJXdxnB$ cat ciphertext >> x
krypton2@krypton:/tmp/tmp.8eNUJXdxnB$ echo "" >> x
krypton2@krypton:/tmp/tmp.8eNUJXdxnB$ cat x
ABCDEFGHIJKLMNOPQRSTUVWXYZ
MNOPQRSTUVWXYZABCDEFGHIJKL
```

Now we can decrypt it.

```sh
krypton2@krypton:/tmp/tmp.8eNUJXdxnB$ cat /krypton/krypton2/krypton3 
OMQEMDUEQMEK
```

O > C
M > E
Q > A
E > S
M > A
D > R
U > I
E > S
Q > E
M > A
E > S
K > Y

CAESARISEASY

