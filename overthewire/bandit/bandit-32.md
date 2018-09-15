Looks like an escape level. Whatever we enter, it runs it in uppercase.

WELCOME TO THE UPPERCASE SHELL
>> ls
sh: 1: LS: not found
>> $shell
WELCOME TO THE UPPERCASE SHELL

We're going to need to escape the shell without any lowercase letters. I will
have to admit that this took me a while. I found the solution by chance while I
was playing around with shell variables.

>> $0
$ ls
uppershell
$ whoami 
bandit33

It looks like we're already bandit33. All that's left to do is get the password
for it.

$ cat /etc/bandit_pass/bandit33
c9c3199ddf4121b10cf581a98d51caee
