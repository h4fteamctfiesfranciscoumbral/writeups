We're given that the file is somewhere on the server and is owned by the user
bandit7, group bandit6, and is 33 bytes.

First, we're going to need to navigate to the root directory (/) since it's
somewhere on the SERVER. Then, we can use "find" again.

bandit6@bandit:~$ cd /
bandit6@bandit:/$ find -user bandit7 -group bandit6 -size 33c
find: './etc/ssl/private': Permission denied
find: './etc/polkit-1/localauthority': Permission denied
find: './run/lxcfs': Permission denied
find: './run/user/11028': Permission denied
find: './run/user/11016': Permission denied
-- snip --

Okay. Problem. We're getting a bunch of permission denieds. Let's filter all
these out by redirecting errors to /dev/null.

bandit6@bandit:/$ find -user bandit7 -group bandit6 -size 33c 2>/dev/null
./var/lib/dpkg/info/bandit7.password

Found it!

bandit6@bandit:/$ cat ./var/lib/dpkg/info/bandit7.password
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
