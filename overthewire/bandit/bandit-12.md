We have hexdump of a repeatedly compressed file.

First things first, let's create a temporary workplace and copy the file there.
We can use "mktemp" passing the "-d" (directory) flag to make a temporary
directory, then "cp" (copy) to copy the file there.

bandit12@bandit:~$ ls
data.txt
bandit12@bandit:~$ mktemp -d
/tmp/tmp.9OQhDJmUQX
bandit12@bandit:~$ cp data.txt /tmp/tmp.9OQhDJmUQX/
bandit12@bandit:~$ cd /tmp/tmp.9OQhDJmUQX/
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ ls
data.txt

Alright. Now let's reverse the hexdump. We can use "xxd" passing the "-r" flag
(reverse) to reverse the hexdump into its original file.

bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ xxd -r data.txt data
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ ls
data  data.txt

Now let's find out what kind of a file it is.

bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ file data
data: gzip compressed data, was "data2.bin", last modified: Thu Dec 28 13:34:36 2017, max compression, from Unix

gzip. We can use "gunzip" for this. It requires a ".gz" extension, though, so
we have to add that extension first.

bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ mv data data.gz
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ gunzip data.gz 
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ ls
data  data.txt

Now let's find out what kind of a file it is.

bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ file data
data: bzip2 compressed data, block size = 900k 

bzip2. Easy enough. We can use "bzip2" passing the "-d" (decompress) flag.

bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ bzip2 -d data
bzip2: Can't guess original name for data -- using data.out
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ ls
data.out  data.txt
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ file data.out
data.out: gzip compressed data, was "data4.bin", last modified: Thu Dec 28 13:34:36 2017, max compression, from Unix

gzip again.

bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ mv data.out data.out.gz
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ gunzip data.out.gz 
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ ls
data.out  data.txt
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ file data.out
data.out: POSIX tar archive (GNU)

We have a tar file now. We can use "tar" passing "xf" (extract, file).

bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ tar xf data.out 
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ ls
data.out  data.txt  data5.bin
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ file data5.bin 
data5.bin: POSIX tar archive (GNU)

tar again.

bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ tar xf data5.bin
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ ls
data.out  data.txt  data5.bin  data6.bin
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k

bzip2 again.

bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ bzip2 -d data6.bin
bzip2: Can't guess original name for data6.bin -- using data6.bin.out
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ ls
data.out  data.txt  data5.bin  data6.bin.out
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ file data6.bin.out
data6.bin.out: POSIX tar archive (GNU)

tar again.

bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ tar xf data6.bin.out
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ ls
data.out  data.txt  data5.bin  data6.bin.out  data8.bin
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ file data8.bin
data8.bin: gzip compressed data, was "data9.bin", last modified: Thu Dec 28 13:34:36 2017, max compression, from Unix

gzip again.

bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ mv data8.bin data8.bin.gz
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ gunzip data8.bin.gz 
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ ls
data.out  data.txt  data5.bin  data6.bin.out  data8.bin
bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ file data8.bin
data8.bin: ASCII text

Finally, we're done decompressing.

bandit12@bandit:/tmp/tmp.9OQhDJmUQX$ cat data8.bin 
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
