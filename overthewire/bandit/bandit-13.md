We're given the ssh key to access the next level. Easy enough. We can pass "-i"
followed by the key to use it instead of a password.

bandit13@bandit:~$ ls
sshkey.private
bandit13@bandit:~$ ssh -i sshkey.private bandit14@localhost
