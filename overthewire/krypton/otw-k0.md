We're given the base64 encoded password. Simple enough. We can use "base64"
passing "-d" (decode) as a flag in order to decode it into its plaintext.

```sh
$ echo "S1JZUFRPTklTR1JFQVQ=" | base64 -d 
KRYPTONISGREAT
```
