Similar to the last level, but now we have to use SSL. This is simple enough.
We can use "openssl" passing "s_client" and "-connect" followed by the host and
port in order to connect to a host on a certain port using SSL.

```sh
bandit15@bandit:~$ openssl s_client -connect localhost:30001
-snip-
BfMYroe26WYalil77FoDi9qh59eK5xNr
HEARTBEATING
read R BLOCK
```

We're getting a "HEARTBEATING". We need to pass "-ign_eof".

```sh
bandit15@bandit:~$ openssl s_client -ign_eof -connect localhost:30001
-snip-
BfMYroe26WYalil77FoDi9qh59eK5xNr
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd

closed
```
