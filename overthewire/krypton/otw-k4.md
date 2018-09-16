Let's see what we're working with.

```sh
krypton4@krypton:~$ cd /krypton/krypton4/
krypton4@krypton:/krypton/krypton4$ ls
HINT  README  found1  found2  krypton5
```

Let's see what the hint has to say.

```sh
krypton4@krypton:/krypton/krypton4$ cat HINT 
Frequency analysis will still work, but you need to analyse it
by "keylength".  Analysis of cipher text at position 1, 6, 12, etc
should reveal the 1st letter of the key, in this case.  Treat this as
6 different mono-alphabetic ciphers...

Persistence and some good guesses are the key!
```

Looks like we're dealing with a Vigenere cipher. We also know the key length!

There's a tool hosted on the same site as the previous level that I use a lot
for breaking Vigeneres during CTFs. https://www.dcode.fr/vigenere-cipher

From this, we get that the key is "FREKEY".

Let's get the ciphertext...

```sh
krypton4@krypton:/krypton/krypton4$ cat krypton5 
HCIKV RJOX
```

...and decrypt it using a Vigenere cipher and the key "FREKEY".

We get "CLEAR TEXT". The password is "CLEARTEXT".
