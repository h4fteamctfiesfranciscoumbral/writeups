The file contains rot13 encoded data.

We can use "tr" to turn all characters A-Z to N-Z and A-M (i.e. rotate them 13
spaces) and feed it the data file as an input.

```sh
bandit11@bandit:~$ ls
data.txt
bandit11@bandit:~$ tr "A-Za-z" "N-ZA-Mn-za-m" < data.txt 
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
```
