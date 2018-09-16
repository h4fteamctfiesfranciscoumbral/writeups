Let's see here...

```sh
krypton6@krypton:~$ cd /krypton/krypton6/
krypton6@krypton:/krypton/krypton6$ ls
HINT1  HINT2  README  encrypt6  keyfile.dat  krypton7  onetime
krypton6@krypton:/krypton/krypton6$ cat HINT*     
The 'random' generator has a limited number of bits, and is periodic.
Entropy analysis and a good look at the bytes in a hex editor will help.

There is a pattern!
8 bit LFSR
```

Let's check out that onetime/ directory.

```sh
krypton6@krypton:/krypton/krypton6$ cd onetime/
krypton6@krypton:/krypton/krypton6/onetime$ ls
cipher1  key1  plain1
krypton6@krypton:/krypton/krypton6/onetime$ cat cipher1 
ABJGGZVHEIKLHMXIZKWZHBAUAPPHSJKHBTYXQPWCLPHSMIVOAKVYYWMQHXMLOIDEZYPURHMJOQSIWHAWESVRWBJTCIWDINKWIJXDMRIPNNRQBUKHDKPACMIQGJEQXXIGWIAARGWPHAXYASYRFAZKFMWWKGKTUHNYLLIESXIOICBAWJMMDEUHBRKTCABLXTCSUYTYELDXKJNWZMLVRFBSFLHQTDXOEVSISWYMYMHYLMSUFJGWJEUDJESTAIPNJPQkrypton6@krypton:/krypton/krypton6/onetime$ cat key1    
ITWASTHEBESTOFTIMESITWASTHEWORSTOFTIMESITWASTHEAGEOFWISDOMITWASTHEAGEOFFOOLISHNESSITWASTHEEPOCHOFBELIEFITWASTHEEPOCHOFINCREDULITYITWASTHESEASONOFLIGHTITWASTHESEASONOFDARKNESSITWASTHESPRINGOFHOPEITWASTHEWINTEROFDESPAIRWEHADEVERYTHINGBEFOREUSWEHADNOTHINGBEF
krypton6@krypton:/krypton/krypton6/onetime$ cat plain1 
SINGOGODDESSTHEANGEROFACHILLESSONOFPELEUSTHATBROUGHTCOUNTLESSILLSUPONTHEACHAEANSMANYABRAVESOULDIDITSENDHURRYINGDOWNTOHADESANDMANYAHERODIDITYIELDAPREYTODOGSANDVULTURESFORSOWERETHECOUNSELSOFJOVEFULFILLEDFROMTHEDAYONWHICHTHESONOFATREUSKINGOFMENANDGREATACHILL
```

Looks like plain1 was encrypted with key1 to create cipher1.

Before I go any further, let's get the actual flag we're trying to decrypt.

```sh
krypton6@krypton:/krypton/krypton6$ cat krypton7 
PNUKLYLWRQKGKBE
```

Let's see if we can find a pattern in the encryption scheme. I'm going to feed
a bunch of As and see if it's a simple one-to-one substitution cipher or if
there's some kind of shifting involved.

First, let's make a temporary directory to work in.

```sh
krypton6@krypton:/krypton/krypton6$ mktemp -d
/tmp/tmp.tcGSQn3rKb
krypton6@krypton:/krypton/krypton6$ cd /tmp/tmp.tcGSQn3rKb
```

Now let's make a file filled with a bunch of As.

```sh
krypton6@krypton:/tmp/tmp.tcGSQn3rKb$ python -c "print 'A'*100" > file
```

Now let's encrypt it and see what the pattern is.

```sh
krypton6@krypton:/tmp/tmp.tcGSQn3rKb$ /krypton/krypton6/encrypt6 file file.out
failed to open keyfile
```

Oops! Forgot to link the file and set permissions like we did previously.

```sh
krypton6@krypton:/tmp/tmp.tcGSQn3rKb$ ln -s /krypton/krypton6/keyfile.dat
krypton6@krypton:/tmp/tmp.tcGSQn3rKb$ chmod 777 .
```

Now let's encrypt it.

```sh
krypton6@krypton:/tmp/tmp.tcGSQn3rKb$ /krypton/krypton6/encrypt6 file file.out
krypton6@krypton:/tmp/tmp.tcGSQn3rKb$ cat file.out 
EICTDGYIYZKTHNSIRFXYCPFUEOCKRNEICTDGYIYZKTHNSIRFXYCPFUEOCKRNEICTDGYIYZKTHNSIRFXYCPFUEOCKRNEICTDGYIYZ
```

It looks like it's repeating every 30 characters.

EICTDGYIYZKTHNSIRFXYCPFUEOCKRN <-30 characters
EICTDGYIYZKTHNSIRFXYCPFUEOCKRN
EICTDGYIYZKTHNSIRFXYCPFUEOCKRN
EICTDGYIYZ

Now let's see what its relationship is with other letters.

```sh
krypton6@krypton:/tmp/tmp.tcGSQn3rKb$ python -c "print 'B'*100" > file
krypton6@krypton:/tmp/tmp.tcGSQn3rKb$ /krypton/krypton6/encrypt6 file file.out
krypton6@krypton:/tmp/tmp.tcGSQn3rKb$ cat file.out 
FJDUEHZJZALUIOTJSGYZDQGVFPDLSOFJDUEHZJZALUIOTJSGYZDQGVFPDLSOFJDUEHZJZALUIOTJSGYZDQGVFPDLSOFJDUEHZJZA
```

FJDUEHZJZALUIOTJSGYZDQGVFPDLSO <- 30 characters
FJDUEHZJZALUIOTJSGYZDQGVFPDLSO
FJDUEHZJZALUIOTJSGYZDQGVFPDLSO
FJDUEHZJZA

Looks like they're all shifted 1 space from A's ciphertext.

I should therefore expect that AB will be EJ.

```sh
krypton6@krypton:/tmp/tmp.tcGSQn3rKb$ echo "AB" > file
krypton6@krypton:/tmp/tmp.tcGSQn3rKb$ /krypton/krypton6/encrypt6 file file.out
krypton6@krypton:/tmp/tmp.tcGSQn3rKb$ cat file.out
EJ
```

Yup! Let's generate the references we'll need to decrypt the password.

```sh
krypton6@krypton:/tmp/tmp.tcGSQn3rKb$ echo "" > file
krypton6@krypton:/tmp/tmp.tcGSQn3rKb$ python
Python 2.7.6 (default, Nov 23 2017, 15:49:48) 
[GCC 4.8.4] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import os
>>> import string
>>> for c in string.ascii_uppercase:
...     l = c*30
...     os.system("echo %s >> file" % l)
... 

krypton6@krypton:/tmp/tmp.tcGSQn3rKb$ /krypton/krypton6/encrypt6 file file.out
krypton6@krypton:/tmp/tmp.tcGSQn3rKb$ cat file.out
EICTDGYIYZKTHNSIRFXYCPFUEOCKRNFJDUEHZJZALUIOTJSGYZDQGVFPDLSOGKEVFIAKABMVJPUKTHZAERHWGQEMTPHLFWGJBLBCNWKQVLUIABFSIXHRFNUQIMGXHKCMCDOXLRWMVJBCGTJYISGOVRJNHYILDNDEPYMSXNWKCDHUKZJTHPWSKOIZJMEOEFQZNTYOXLDEIVLAKUIQXTLPJAKNFPFGRAOUZPYMEFJWMBLVJRYUMQKBLOGQGHSBPVAQZNFGKXNCMWKSZVNRLCMPHRHITCQWBRAOGHLYODNXLTAWOSMDNQISIJUDRXCSBPHIMZPEOYMUBXPTNEORJTJKVESYDTCQIJNAQFPZNVCYQUOFPSKUKLWFTZEUDRJKOBRGQAOWDZRVPGQTLVLMXGUAFVESKLPCSHRBPXEASWQHRUMWMNYHVBGWFTLMQDTISCQYFBTXRISVNXNOZIWCHXGUMNREUJTDRZGCUYSJTWOYOPAJXDIYHVNOSFVKUESAHDVZTKUXPZPQBKYEJZIWOPTGWLVFTBIEWAULVYQAQRCLZFKAJXPQUHXMWGUCJFXBVMWZRBRSDMAGLBKYQRVIYNXHVDKGYCWNXASCSTENBHMCLZRSWJZOYIWELHZDXOYBTDTUFOCINDMASTXKAPZJXFMIAEYPZCUEUVGPDJOENBTUYLBQAKYGNJBFZQADVFVWHQEKPFOCUVZMCRBLZHOKCGARBEWGWXIRFLQGPDVWANDSCMAIPLDHBSCFXHXYJSGMRHQEWXBOETDNBJQM
```

Oof. This is an ugly file. Let's insert a newline every 30 characters.

```sh
krypton6@krypton:/tmp/tmp.tcGSQn3rKb$ sed -e "s/.\{30\}/&\n/g" < file.out
EICTDGYIYZKTHNSIRFXYCPFUEOCKRN
FJDUEHZJZALUIOTJSGYZDQGVFPDLSO
GKEVFIAKABMVJPUKTHZAERHWGQEMTP
HLFWGJBLBCNWKQVLUIABFSIXHRFNUQ
IMGXHKCMCDOXLRWMVJBCGTJYISGOVR
JNHYILDNDEPYMSXNWKCDHUKZJTHPWS
KOIZJMEOEFQZNTYOXLDEIVLAKUIQXT
LPJAKNFPFGRAOUZPYMEFJWMBLVJRYU
MQKBLOGQGHSBPVAQZNFGKXNCMWKSZV
NRLCMPHRHITCQWBRAOGHLYODNXLTAW
OSMDNQISIJUDRXCSBPHIMZPEOYMUBX
PTNEORJTJKVESYDTCQIJNAQFPZNVCY
QUOFPSKUKLWFTZEUDRJKOBRGQAOWDZ
RVPGQTLVLMXGUAFVESKLPCSHRBPXEA
SWQHRUMWMNYHVBGWFTLMQDTISCQYFB
TXRISVNXNOZIWCHXGUMNREUJTDRZGC
UYSJTWOYOPAJXDIYHVNOSFVKUESAHD
VZTKUXPZPQBKYEJZIWOPTGWLVFTBIE
WAULVYQAQRCLZFKAJXPQUHXMWGUCJF
XBVMWZRBRSDMAGLBKYQRVIYNXHVDKG
YCWNXASCSTENBHMCLZRSWJZOYIWELH
ZDXOYBTDTUFOCINDMASTXKAPZJXFMI
AEYPZCUEUVGPDJOENBTUYLBQAKYGNJ
BFZQADVFVWHQEKPFOCUVZMCRBLZHOK
CGARBEWGWXIRFLQGPDVWANDSCMAIPL
DHBSCFXHXYJSGMRHQEWXBOETDNBJQM
```

Alright! Let's start decrypting!

Key:
```
 |01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30
-+-----------------------------------------------------------------------------------------
A| E  I  C  T  D  G  Y  I  Y  Z  K  T  H  N  S  I  R  F  X  Y  C  P  F  U  E  O  C  K  R  N
B| F  J  D  U  E  H  Z  J  Z  A  L  U  I  O  T  J  S  G  Y  Z  D  Q  G  V  F  P  D  L  S  O
C| G  K  E  V  F  I  A  K  A  B  M  V  J  P  U  K  T  H  Z  A  E  R  H  W  G  Q  E  M  T  P
D| H  L  F  W  G  J  B  L  B  C  N  W  K  Q  V  L  U  I  A  B  F  S  I  X  H  R  F  N  U  Q
E| I  M  G  X  H  K  C  M  C  D  O  X  L  R  W  M  V  J  B  C  G  T  J  Y  I  S  G  O  V  R
F| J  N  H  Y  I  L  D  N  D  E  P  Y  M  S  X  N  W  K  C  D  H  U  K  Z  J  T  H  P  W  S
G| K  O  I  Z  J  M  E  O  E  F  Q  Z  N  T  Y  O  X  L  D  E  I  V  L  A  K  U  I  Q  X  T
H| L  P  J  A  K  N  F  P  F  G  R  A  O  U  Z  P  Y  M  E  F  J  W  M  B  L  V  J  R  Y  U
I| M  Q  K  B  L  O  G  Q  G  H  S  B  P  V  A  Q  Z  N  F  G  K  X  N  C  M  W  K  S  Z  V
J| N  R  L  C  M  P  H  R  H  I  T  C  Q  W  B  R  A  O  G  H  L  Y  O  D  N  X  L  T  A  W
K| O  S  M  D  N  Q  I  S  I  J  U  D  R  X  C  S  B  P  H  I  M  Z  P  E  O  Y  M  U  B  X
L| P  T  N  E  O  R  J  T  J  K  V  E  S  Y  D  T  C  Q  I  J  N  A  Q  F  P  Z  N  V  C  Y
M| Q  U  O  F  P  S  K  U  K  L  W  F  T  Z  E  U  D  R  J  K  O  B  R  G  Q  A  O  W  D  Z
N| R  V  P  G  Q  T  L  V  L  M  X  G  U  A  F  V  E  S  K  L  P  C  S  H  R  B  P  X  E  A
O| S  W  Q  H  R  U  M  W  M  N  Y  H  V  B  G  W  F  T  L  M  Q  D  T  I  S  C  Q  Y  F  B
P| T  X  R  I  S  V  N  X  N  O  Z  I  W  C  H  X  G  U  M  N  R  E  U  J  T  D  R  Z  G  C
Q| U  Y  S  J  T  W  O  Y  O  P  A  J  X  D  I  Y  H  V  N  O  S  F  V  K  U  E  S  A  H  D
R| V  Z  T  K  U  X  P  Z  P  Q  B  K  Y  E  J  Z  I  W  O  P  T  G  W  L  V  F  T  B  I  E
S| W  A  U  L  V  Y  Q  A  Q  R  C  L  Z  F  K  A  J  X  P  Q  U  H  X  M  W  G  U  C  J  F
T| X  B  V  M  W  Z  R  B  R  S  D  M  A  G  L  B  K  Y  Q  R  V  I  Y  N  X  H  V  D  K  G
U| Y  C  W  N  X  A  S  C  S  T  E  N  B  H  M  C  L  Z  R  S  W  J  Z  O  Y  I  W  E  L  H
V| Z  D  X  O  Y  B  T  D  T  U  F  O  C  I  N  D  M  A  S  T  X  K  A  P  Z  J  X  F  M  I
W| A  E  Y  P  Z  C  U  E  U  V  G  P  D  J  O  E  N  B  T  U  Y  L  B  Q  A  K  Y  G  N  J
X| B  F  Z  Q  A  D  V  F  V  W  H  Q  E  K  P  F  O  C  U  V  Z  M  C  R  B  L  Z  H  O  K
Y| C  G  A  R  B  E  W  G  W  X  I  R  F  L  Q  G  P  D  V  W  A  N  D  S  C  M  A  I  P  L
Z| D  H  B  S  C  F  X  H  X  Y  J  S  G  M  R  H  Q  E  W  X  B  O  E  T  D  N  B  J  Q  M
```

Ciphertext:
```
PNUKLYLWRQKGKBE
```

Decrypting this is easy, really. P is the first letter in the sequence. In the
key, where P is the first letter in the sequence is L. N is the second letter
in the sequence. In the key, where N is the second letter is F. And so on and
so forth.

```
01 02 03 04 05 06 07 08 09 10 11 12 13 14 15
P  N  U  K  L  Y  L  W  R  Q  K  G  K  B  E
--------------------------------------------
L  F  S  R  I  S  N  O  T  R  A  N  D  O  M
```

LFSRISNOTRANDOM 
