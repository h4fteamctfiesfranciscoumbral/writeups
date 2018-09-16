Let's have a look...

```sh
krypton3@krypton:~$ cd /krypton/krypton3/
krypton3@krypton:/krypton/krypton3$ ls
HINT1  HINT2  README  found1  found2  found3  krypton4
```

What do the hints have to say?

```sh
krypton3@krypton:/krypton/krypton3$ cat HINT1
Some letters are more prevalent in English than others.
krypton3@krypton:/krypton/krypton3$ cat HINT2
"Frequency Analysis" is your friend.
```

Looks like we're going to need to use a frequency analysis tool. This will tell
us the frequency of each character. Then, all we'll need to do is match the
found frequencies of letters in the 3 found files with letter frequency in
English. We can derive how many spaces the alphabet was shifted in order to
produce the flag using this method.

```sh
krypton3@krypton:/krypton/krypton3$ cat found*
CGZNL YJBEN QYDLQ ZQSUQ NZCYD SNQVU BFGBK GQUQZ QSUQN UZCYD...
-snip-
```

I'm going to punch all of this into a popular frequency analysis tool available
over at http://jnicholl.org/Cryptanalysis/Tools/FrequencyAnalysis1.php.

The letters, organized by frequency, are...

S	456	Z	132	L	60				
Q	340	V	130	A	55				
J	301	W	129	F	28				
U	257	M	86	I	19				
B	246	Y	84	O	12				
N	240	T	75	H	4				
G	227	X	71	R	4				
C	227	K	67	P	2				
D	210	E	64	

In English, the frequencies of letters from greatest to least are listed in a
study here: http://pi.math.cornell.edu/~mec/2003-2004/cryptography/subs/frequencies.html

Based on this, we can make the assumptions that

This isn't the only hint they gave us. They also gave us the hint that the key
was in English.

The jump from the most common letter, E, to the most common letter in the
ciphertext, S, leads me to believe that it was rotated 14 spaces.

Using the alphabetical substitution tool over at,
https://www.guballa.de/substitution-solver, we find that the mappings are:

abcdefghijklmnopqrstuvwxyz 
qazwsxedcrfvtgbyhnujmikolp

We can use this to decrypt the flag.

```sh
krypton3@krypton:/krypton/krypton3$ cat krypton4 
KSVVW BGSJD SVSIS VXBMN YQUUK BNWCU ANMJS
```

KSVVW BGSJD SVSIS VXBMN YQUUK BNWCU ANMJS
WELLD ONETH ELECE IFOUR PASSW ORDIS BRUTE

WELLDONETHELECEIFOURPASSWORDISBRUTE
