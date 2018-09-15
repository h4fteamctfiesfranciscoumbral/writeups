We need to submit the current password to localhost:30000.

First, let's get the current password.

bandit14@bandit:~$ cat /etc/bandit_pass/bandit14 
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e

Now let's open up a connection to localhost:30000 and feed it the password.

bandit14@bandit:~$ nc localhost 30000
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
